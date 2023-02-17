# Firefly
Docker compose file and env templates for self-hosted Firefly III instance
## Deployment
1. Clone repo
```
git clone git@github.com:aryzhk0v/firefly.git
```
2. Rename env files
```
mv env-app.example .env-app
mv env-db.example .env-db
```
3. Set environment variables:  
`.env-app`:
- APP_KEY (32 character long string)
- TZ
- DB_PASSWORD
- APP_URL  
`.env-db`:
- MYSQL_PASSWORD
4. Start containers
```
docker-compose -f docker-compose.yml up -d
```
## Backups
https://docs.firefly-iii.org/firefly-iii/advanced-installation/backup/

## Notes

- Container port for `app` container should always be 8080 because it's hardcoded in Apache vhost inside the container
- If there are minor bugs when using reverse proxy (such as Cloudflare). e.g. graphs are not shown, or GUI elements ignore clicks on them change `TRUSTED_PROXIES` variable to `TRUSTED_PROXIES=**` in `.env-app`
