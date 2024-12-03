# Permanently Remove a Leaked .env File from GitHub

## Table of Contents
- [Permanently Remove a Leaked .env File from GitHub](#permanently-remove-a-leaked-env-file-from-github)
  - [Table of Contents](#table-of-contents)
  - [Revoke any leaked credentials](#revoke-any-leaked-credentials)
  - [Remove the file and commit the changes](#remove-the-file-and-commit-the-changes)
  - [Remove the .env file from history with filter-branch](#remove-the-env-file-from-history-with-filter-branch)
  - [Force push the changes to github](#force-push-the-changes-to-github)
  - [Clean up the local repository](#clean-up-the-local-repository)
  - [References](#references)


## Revoke any leaked credentials
if you have accidentally leaked any credentials, revoke them immediately. This will prevent unauthorized access to your accounts.

## Remove the file and commit the changes
Remove the leaked file from your local repository and commit the changes.

```bash
git rm --cached .env
echo ".env" >> .gitignore
git add .gitignore
git commit -m "Remove leaked .env file"
```

## Remove the .env file from history with filter-branch
```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch .env' --prune-empty --tag-name-filter cat -- --all
```
`filter-branch` will rewrite the history of your repository to remove the `.env` file from all commits.

- `--force`: This option forces the rewrite even if the branch is already filtered.
- `--index-filter 'git rm --cached --ignore-unmatch .env'`: This option specifies a command to run on each commit. Here, it removes the .env file from the index (staging area) if it exists.
- `--prune-empty`: This option removes any commits that become empty (i.e., have no changes) after the filter is applied.
- `--tag-name-filter cat`: This option ensures that tags are rewritten to point to the corresponding rewritten commits.
`-- --all`: This option specifies that the filter should be applied to all branches and tags.

## Force push the changes to github
```bash
git push origin --force --all
git push --force --tags
```

## Clean up the local repository
```bash
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```


## References
- [How to remove a leaked .env file from GitHub permanently](https://dev.to/kodebae/how-to-remove-a-leaked-env-file-from-github-permanently-3lei)
- [Exposing secrets on GitHub: What to do after leaking credentials and API keys](https://blog.gitguardian.com/leaking-secrets-on-github-what-to-do/)
