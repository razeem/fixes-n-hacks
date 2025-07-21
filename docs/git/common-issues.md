# Git Common Issues

## Bitbucket: Link repo commit messages to task ID
- Go to Repository Settings > Links > Create New Link
- Link URL: `https://4spots.me/projects/<project-id in intranet>/tasks/\1`
- Link TEXT: `<project-code for the project>-(\d+)`

## Issues
### Pull not working, branch diverged
```
git reset --hard origin/develop
```
### Push/pull stuck (slow ssh)
- Switch to https in `.git/config`:
```
[remote "origin"]
url = https://razeem4spots@bitbucket.org/team4spots/abo001.git
```
### Different SSH keys for different projects
- Create SSH key: `ssh-keygen -f ~/.ssh/personal`
- Create/edit `~/.ssh/config`:
```
Host bitbucket.org
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_rsa
Host personal
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/personal
```
- Clone/set remote:
```
git clone personal:star-jet/ppr001-backend.git
git remote set-url origin personal:star-jet/ppr001-backend.git
```
