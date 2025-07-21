# Angular Dummy Server

## Server Setup for Angular

Install PHP and enable `mod_proxy` and `mod_proxy_http` in Apache.

Example Apache vhost config:
```apache
<VirtualHost *:80>
  ServerName ert-angular.local.com
  DocumentRoot "/var/www/html/angular-ert"
  ProxyPass "/jwt" "http://portalert002.4spotsdemo.com/jwt"
  ProxyPass "/api" "http://portalert002.4spotsdemo.com/api"
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
        "name": "Al Waleed Bin Talal",
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
providers: [UserDetailsService],
```
