# Common Git Commands

## SSH Key Management for Multiple Projects

### Create SSH Keys
```sh
ssh-keygen -f ~/.ssh/personal
```

### Configure SSH Agent
```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/personal
```

### Edit SSH Config (~/.ssh/config)
```sh
Host bitbucket.org
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_rsa
Host personal
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/personal
```

## Setting Git Remotes

### HTTPS Remote Example
```ini
[remote "origin"]
url = https://<USER>@bitbucket.org/<TEAM>/<REPO>.git
```

### SSH Remote Example
```ini
[remote "origin"]
url = git@bitbucket.org:<TEAM>/<REPO>.git
```

### Clone and Set Remote
```sh
git clone personal:<TEAM>/<REPO>.git
git remote set-url origin personal:<TEAM>/<REPO>.git
```

## Bitbucket Integration

### Link Repo Commit Messages to Task ID
- Go to Repository Settings > Links > Create New Link

- Link URL: `https://<COMPANY>.me/projects/<project-id>/tasks/\1`
- Link TEXT: `<project-code>-(\d+)`
## Advanced Git Commands

### Amend Last Commit
```sh
git commit --amend -m "New commit message"
```
#### Commit With No Edit
```sh
git commit --amend --no-edit
```

### Cherry-pick a Commit from Another Branch
```sh
git cherry-pick <commit-hash>
```

### Rebase Instead of Merge
- Start an interactive rebase:
```sh
git rebase -i <base-branch>
```
- Rebase your feature branch onto main:
```sh
git checkout feature-branch
git rebase main
```
- Continue after resolving conflicts:
```sh
git rebase --continue
```
- Abort a rebase:
```sh
git rebase --abort
```
