# Git

You can use the `git log` command with the `--grep` option to search for a specific phrase in the commit history. Here's an example:

```bash
git log --all --grep='Your Phrase Here'
```

Replace `'Your Phrase Here'` with the phrase you want to search for. This command will search through all branches of your repository for the specified phrase in the commit messages. If you want to search the commit changes instead of the commit message, you can use:

```bash
git log -S 'Your Phrase Here'
```

This will show commits that added or removed the specified phrase. Remember to replace `'Your Phrase Here'` with the phrase you're looking for.

You can use the `git log` command with the `-S` option to search for a specific text in the changes made by the commits. Here's an example:

```bash
git log -S '[download] Destination: '
```

This command will show commits that added or removed the specified text in the files. Remember to replace `'[download] Destination: '` with the text you're looking for. This command will search through all branches of your repository for the specified text in the commit changes. If you want to limit the search to a specific branch, you can specify the branch name after `git log`. For example:

```bash
git log <branch-name> -S '[download] Destination: '
```

Replace `<branch-name>` with the name of the branch you want to search in. This command will search only in the specified branch for the text in the commit changes.

To count the total number of commits returned by the `git log -S '[download] Destination: '` command, you can pipe the output to `wc -l`, which counts the number of lines. Each commit is represented by a line starting with 'commit' in the `git log` output. Here's how you can do it:

- Bash

```bash
git log --pretty=oneline -S '[download] Destination: ' | wc -l
```

- PowerShell Corel

```pwsh
git log --pretty=oneline -S '[download] Destination: ' | Measure-Object -Line
```

This command will return the total number of commits that added or removed the specified text. Please replace `'[download] Destination: '` with the text you're looking for. Note that this command counts the commits across all branches. If you want to limit the search to a specific branch, you can specify the branch name after `git log`. For example:

```bash
git log <branch-name> --pretty=oneline -S '[download] Destination: ' | wc -l
```

Replace `<branch-name>` with the name of the branch you want to search in. This command will count the commits only in the specified branch that added or removed the specified text. Please note that this command needs to be run in the terminal of your local machine where the git repository is located.

## Development

```pwsh
➜ .\.venv\Scripts\Activate.ps1
➜ py -m pip install pipdeptree
➜ pip install uv
➜ pipdeptree 
➜ pipdeptree --exclude pip,pipdeptree,setuptools,wheel,uv --warn silence | Select-String -Pattern '^\w+'  > requirements.txt
➜ pipdeptree -f --warn silence > locked-requirements.txt

```

### How to use

```pwsh
➜ uv pip install -r requirements.txt
➜ uv pip sync requirements.txt
```

### Git search

You can use the `awk` command in combination with `git log` to extract the commit hash, author, date, and YouTube song ID. Here's an example command:

```bash
git log -S 'Bill Medley' | awk '/commit/ {print "commit: "$2} /Author:/ {print "Author: "$2" "$3" "$4} /Date:/ {print "Date: "$3" "$4" "$5" "$6" "$7} /^    Add/ {split($0,a,"_"); print "Song: "a[2]}'
```

This command will output the desired information in the format you specified. Please replace `'Bill Medley'` with the actual string you want to search for in your Git log. Note that this command assumes that the YouTube song ID is always after the last underscore (`_`) in the commit message. If the format of your commit message changes, you may need to adjust the command accordingly.

#### Powershell

Sure, here's how you can achieve the same result using PowerShell:

```pwsh
git log -S '[download] Destination: ' | ForEach-Object {
    if ($_ -match 'commit (.*)') { "commit: $($matches[1])" }
    elseif ($_ -match 'Author: (.*)') { "Author: $($matches[1])" }
    elseif ($_ -match 'Date:   (.*)') { "Date: $($matches[1])" }
    elseif ($_ -match 'Add (.*),') { $song = $_.Split('_')[-1]; "Song: $song" }
}
```

This script will output the commit hash, author, date, and YouTube song ID in the format you specified. Please replace `'Bill Medley'` with the actual string you want to search for in your Git log. Note that this command assumes that the YouTube song ID is always after the last underscore (`_`) in the commit message. If the format of your commit message changes, you may need to adjust the command accordingly.

```pwsh
git log -S '[download] Destination: ' | ForEach-Object {
    switch -Regex ($_) {
        'commit (.*)' { "commit: $($matches[1])" }
        'Author: (.*)' { "Author: $($matches[1])" }
        'Date:   (.*)' { "Date: $($matches[1])" }
        'Add (.*),' { $song = $_.Split('_')[-1]; "Song: $song" }
    }
}
```
