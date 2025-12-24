## Annie's Birthday Site

Minimal static site for Annika's scavenger hunt. The repo lives in `/home/ryan/Documents/projects/anniebday` and is served directly by Apache.

### 1. Place repo on server

```bash
git clone <repo-url> /home/ryan/Documents/projects/anniebday
cd /home/ryan/Documents/projects/anniebday
```

### 2. Allow Apache to read the files

```bash
chmod o+x /home/ryan
sudo chgrp -R www-data /home/ryan/Documents/projects/anniebday
sudo chmod -R 750 /home/ryan/Documents/projects/anniebday
```

### 3. Link the provided Apache vhost and enable it

```bash
sudo ln -s /home/ryan/Documents/projects/anniebday/apache-site.conf /etc/apache2/sites-available/anniebday.conf
sudo a2ensite anniebday.conf
sudo a2dissite 000-default.conf
sudo systemctl reload apache2
```

### 4. Serve over Tailscale

1. Install Tailscale on the server: `curl -fsSL https://tailscale.com/install.sh | sh`
2. Authenticate: `sudo tailscale up`
3. Note the Tailscale IP (`tailscale ip -4`) and browse `http://<tailscale-ip>/` from any device on your tailnet.

### 5. Update the site

```bash
cd /home/ryan/Documents/projects/anniebday
git pull
sudo systemctl reload apache2
```

Optional: Use `sudo apachectl -S` to confirm only the birthday vhost is active. When finished with the server, you can disable the site via `sudo a2dissite anniebday.conf && sudo systemctl reload apache2`.
