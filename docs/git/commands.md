# Common Commands

### Set Different SSH keys for different projects
- Switch to https in `.git/config`:
```
[remote "origin"]
url = https://<USER>@bitbucket.org/<TEAM>/<REPO>.git
```

- Or, use SSH:
```
[remote "origin"]
url = git@bitbucket.org:<TEAM>/<REPO>.git
```

- Create SSH key: `ssh-keygen -f ~/.ssh/personal`

- Add to ssh-agent:
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/personal
```

- Clone/set remote:
```
git clone personal:<TEAM>/<REPO>.git
git remote set-url origin personal:<TEAM>/<REPO>.git
```
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
git clone personal:<TEAM>/<REPO>.git
git remote set-url origin personal:<TEAM>/<REPO>.git
```

## Bitbucket: Link repo commit messages to task ID
- Go to Repository Settings > Links > Create New Link
- Link URL: `https://<COMPANY>.me/projects/<project-id>/tasks/\1`
- Link TEXT: `<project-code>-(\d+)`
