# Angular Dummy Server

## Server Setup for Angular

Install PHP and enable `mod_proxy` and `mod_proxy_http` in Apache.

Example Apache vhost config:
```apache
<VirtualHost *:80>
  ServerName <PROJECT>.local.com
  DocumentRoot "/var/www/html/<PROJECT>"
  ProxyPass "/jwt" "http://<API_SERVER>/jwt"
  ProxyPass "/api" "http://<API_SERVER>/api"
</VirtualHost>
```

## Project Setup
```sh
git clone ...
cd folder
npm install
```

## Setup a Dummy Server in Angular
Install json-server:
```sh
npm install json-server
```

### Example proxy.config.json
```json
{
  "/demo/*": {
    "target": "http://localhost:3000",
    "secure": false,
    "changeOrigin": true
  },
  "/api/*": {
    "target": "http://192.168.0.113",
    "secure": false,
    "changeOrigin": true
  }
}
```

### Example db.json
```json
{
  "header": {
    "status": true,
    "data": {
      "userDetails": {
        "name": "<USER_NAME>",
        "imageUrl": "http://localhost:4200/assets/images/user.jpg"
      },
      "menu": [
        { "child": false, "title": "My Menu 1", "url": "/" },
        { "child": false, "title": "My Menu 2", "url": "/" }
      ]
    }
  }
}
```

## Centralize URLs
```typescript
export const URLS = {
  header: '/demo/header'
};
```

## Fetch Values from API
```typescript
import { Component, OnInit } from '@angular/core';
import { Header } from './header';
import { HttpClient } from '@angular/common/http';
import { URLS } from '../core/env/urls';

@Component({
 selector: 'app-header',
 templateUrl: './header.component.html',
 styleUrls: ['./header.component.scss']
})
export class HeaderComponent implements OnInit {
  header: Header;
  constructor(private httpClient: HttpClient) { }
  ngOnInit() { this.getHeader(); }
  private getHeader() {
    this.httpClient.get(URLS.header)
      .subscribe((d: { status: boolean; data?: Header }) => {
        if (d.status) this.header = d.data;
      }, err => {
        console.log(err);
        alert('could not fetch header');
      });
  }
}
```

- `subscribe()` takes two params: success and error handlers.

## Use a Service for Shared Data
Generate a service:
```sh
ng g s UserDetails
```
Add to `app.module.ts`:
```typescript
providers: [<SERVICE_NAME>],
```

## Bitbucket: Link repo commit messages to task ID
- Go to Repository Settings > Links > Create New Link
- Link URL: `https://<COMPANY>.me/projects/<project-id>/tasks/\1`
- Link TEXT: `<project-code>-(\d+)`

## Git Setup

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

## File Permission Issues on Mac

- Change ownership:
```
sudo chown <user-name>:<group-name> -R <file-path>
```
- Change permission:
```
sudo chmod 755 -R <file-path>
```
