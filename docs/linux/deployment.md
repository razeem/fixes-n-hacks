# Server Deployment

## Common deployment issues while SSL
- Modify the Vhost as below:
```
<VirtualHost *:443>
 ServerName <PROJECT>.local.com
 DocumentRoot "/var/www/html/<PROJECT>"
 SSLProxyEngineOn
 ProxyPass "/jwt" "https://<API_SERVER>/jwt"
 ProxyPass "/api" "https://<API_SERVER>/api"
</VirtualHost>
```

## CURL commands
```
curl -sILXGET dev-selfservice.fmservice.com
```

## Live reloading not working issue
```
sudo sysctl fs.inotify.max_user_watches=524288 && sudo sysctl -p --system
```

## File handling
- Change ownership:
```
sudo chown <user-name>:<group-name> -R <file-path>
```
- Change permission:
```
sudo chmod 755 -R /var/www/html/
```
- Move/rename/copy/delete/zip/unzip files:
```
sudo mv {old-file} {new-file}
sudo cp -i -r /media/projects/hyn007 /var/www/html/hyn
rm {file-name}
zip -r "archive-$(date +"%Y-%m-%d").zip" <folder>
unzip file.zip -d destination_folder
du -sh *
```
- Kill a process:
```
kill -9 $(lsof -t -i:4200)
```
