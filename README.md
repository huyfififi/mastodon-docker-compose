This repository contains configuration files for running a Mastodon server at [ocalaavenue.net](https://ocalaavenue.net). These configurations are based on those from the official Mastodon repository: [mastodon/mastodon](https://github.com/mastodon/mastodon).

## Certificate Renewal with Let's Encrypt

This setup uses webroot authentication, which allows certificate renewal without stopping the server. Certbot writes challenge files to `/var/www/certbot`, which nginx serves automatically.

### Initial Setup

Before the first certificate issuance, create the webroot directory structure:

```sh
sudo mkdir -p /var/www/certbot/.well-known/acme-challenge
sudo chmod -R 755 /var/www/certbot
```

### Initial Certificate Issuance

For the first time obtaining a certificate:

```sh
sudo certbot certonly --webroot -w /var/www/certbot -d ocalaavenue.net
```

### Check the Current Certificate Status

```sh
sudo certbot certificates
```

### Simulate a Renewal (Dry Run)

```sh
sudo certbot renew --dry-run
```

### Renew the Certificates

```sh
sudo certbot renew
```

The renewal process will work automatically without stopping nginx or any other services. After renewal, you may need to reload nginx to use the new certificates:

```sh
docker compose exec nginx nginx -s reload
```

Or restart the nginx container:

```sh
docker compose restart nginx
```

### Automatic Renewal

Certbot typically sets up automatic renewal via systemd timer or cron. To verify:

```sh
sudo systemctl status certbot.timer
```

Or check cron:

```sh
sudo crontab -l -u root | grep certbot
```

## Database Backup

```
docker exec db pg_dump -Fc -U postgres postgres > dumps/202604161211.dump
```

## Server Specifications ([ocalaavenue.net](https://ocalaavenue.net))

- **VPS**: Amazon Lightsail (4 GB RAM, 2 vCPUs, 80 GB SSD)
- **Domain Name Registrar**: Amazon Route 53
- **Object Storage**: Amazon S3
- **Mail Server**: Gmail (not working now)
