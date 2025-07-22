# Git Common Issues

## Bitbucket: Link repo commit messages to task ID
- Go to Repository Settings > Links > Create New Link
- Link URL: `https://<COMPANY_DOMAIN>/projects/<project-id in intranet>/tasks/\1`
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
url = https://<USER>@bitbucket.org/<TEAM>/<REPO>.git
```
