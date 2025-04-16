This repository contains configuration files for running a Mastodon server at [ocalaavenue.net](https://ocalaavenue.net). These configurations are based on those from the official Mastodon repository: [mastodon/mastodon](https://github.com/mastodon/mastodon).

## Certificate Renewal with Let's Encrypt

Mastodon uses ports that conflict with those required for Let's Encrypt's HTTP-01 challenge, which prevents Certbot from automatically renewing certificates while the server is running. Therefore, you must manually stop the Mastodon server before renewing the certificates.

### Check the Current Certificate Status

```sh
sudo certbot certificates
```

### Simulate a Renewal (Dry Run)

```sh
sudo certbot renew --dry-run
```

### Renew the Certificates

```
sudo certbot renew
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
