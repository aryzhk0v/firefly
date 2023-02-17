# Firefly
Docker compose file and env templates for self-hosted Firefly III instance
## Deployment
1. Clone repo
```
git clone git@github.com:aryzhk0v/firefly.git
```
2. Rename env files
```
mv env.example .env
mv db.env.example .db.env
```
3. Set environment variables:  
`.env`:
- APP_KEY (32 character long string)
- TZ
- DB_PASSWORD
- APP_URL  
`.db.env`:
- MYSQL_PASSWORD
4. Start containers
```
docker-compose -f docker-compose.yml up -d
```
## Backups
### Set up

Add to `/etc/crontab`
```
27 0 * * * your_username /home/your_username/repos/firefly/firefly-iii-backuper.sh backup /home/your_username/backups/firefly/$(date +\%F).tar >> /var/log/firefly-iii-backuper.log 2>&1
```
### Restore
```
/home/your_username/repos/firefly/firefly-iii-backuper.sh restore /home/your_username/backups/firefly/backup_filename.tar
```

## Notes

- Container port for `app` container should always be 8080 because it's hardcoded in Apache vhost inside the container
- If there are minor bugs when using reverse proxy (such as Cloudflare). e.g. graphs are not shown, or GUI elements ignore clicks on them change `TRUSTED_PROXIES` variable to `TRUSTED_PROXIES=**` in `.env`
