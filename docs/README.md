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

## Development

```pwsh
➜ .\.venv\Scripts\Activate.ps1
➜ py -m pip install pipdeptree
➜ pip install uv
➜ pipdeptree 
➜ pipdeptree --exclude pip,pipdeptree,setuptools,wheel --warn silence | Select-String -Pattern '^\w+'  > requirement.txt
➜ pipdeptree -f --warn silence > locked-requirements.txt

```