# nginx-image-server

## Dependencies
- nginx
- ufw

## Setup
Install Nginx + ufw

Set up image server:
```
# Start & Enable NGINX
systemctl start nginx
systemctl enable nginx

# Start & Enable UFW
systemctl start ufw
systemctl enable ufw

# Allow Webserver and SSH ports 
ufw allow 22
ufw allow 80
ufw allow 443

# Enable UFW Rules
ufw enable 
```

Copy contents of etc to `/etc` and var to `/var` on your Linux server

Change `i.davidd.xyz` to your own domain. Do the same with `/etc/nginx/sites-available/i.davidd.xyz`

In `/etc/nginx/sites-available/yourdomain` do the following:
- change `root /var/i.davidd.xyz/;` to `root /var/yourdomain/;`
- change `server_name i.davidd.xyz;` to `server_name yourdomain;`

Symlink `sites-available/yourdomain` to `sites-enabled`:
- `sudo ln -s /etc/nginx/sites-available/yourdomain /etc/nginx/sites-enabled`

Restart nginx so that changes take effect `systemctl restart nginx`. Use `systemctl status nginx` to check if the service loaded and it's working.

You're done with the server side of things! Now you just need to set up HTTPS, which I am not going to cover. You can use Cloudflare for this, no need for certbot.


## Configuring ShareX (Windows)
Set up the destination using your domain. It should look similar to this image:
- `Destinations -> Destination settings -> FTP/FTPS/SFTP`
![alt text](https://i.imgur.com/SOAKJKr.png)
Make sure to test this. If you get `Connected!`, then you're good. If you don't, then you did something wrong.

Set your destination as the default uploader
![alt text](https://i.imgur.com/YFYcQrO.png)

If all goes well, your screenshots will now be uploaded to your domain assuming you have auto upload on. This can be changed in the ShareX settings
![alt text](https://i.imgur.com/D31vmuA.png)

## Linux
Use [this](https://github.com/dps910/scripts/tree/master/screenshot)

## macOS
You can probably use [MagicCap](https://github.com/MagicCap/MagicCap) or make your own shell script for uploading via FTP. My shell script for Linux could be modified to work on macOS.

## Other platforms: BSD, Solaris etc
My shell script might work on these platforms, it depends if they have `maim` or not. I would say it is likely to work on BSD.

## Credit
https://docs.dedicatedmc.io/other/setup-image-sharing-webserver-sharex
