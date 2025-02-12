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
