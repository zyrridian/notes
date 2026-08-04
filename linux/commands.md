```bash
sudo apt update && sudo apt upgrade -y
```

```bash
sudo apt install git -y
```

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

```bash
sudo sh get-docker.sh
```

```bash
sudo usermod -aG docker $USER
```

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

```bash
git clone git@github.com:username/repo-name.git folder-name
```

```bash
ssh-keygen -t ed25519 -f github_actions_deploy_key
```

```bash
cat github_actions_deploy_key.pub >> ~/.ssh/authorized_keys
```

```bash
cat github_actions_deploy_key
```

optional:
```bash
rm github_actions_deploy_key github_actions_deploy_key.pub 
```

update SERVER_SSH_KEY, SERVER_HOST, SERVER_USER, GHCR_PAT, etc.

copy env file, add MIDTRANS_SERVER_KEY

```bash
cd ~/harvest-web
```

```bash
nano .env
```

```bash
MIDTRANS_SERVER_KEY=your_actual_server_key_here
```

github action 

(add/update port if necessary)

---

for domain

add a new "A Record"

install nginx and certbot

```bash
sudo apt install nginx python3-certbot-nginx -y
```

```bash
sudo nano /etc/nginx/sites-available/domain.example.com
```

```bash
server {
    listen 80;
    server_name domain.example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```bash
sudo ln -s /etc/nginx/sites-available/domain.example.com /etc/nginx/sites-enabled/
```

```bash
sudo nginx -t
```

```bash
sudo systemctl restart nginx
```

ssl https

```bash
sudo certbot --nginx -d domain.example.com
```

open port 80/443

```bash

```

```bash

```

```bash

```
