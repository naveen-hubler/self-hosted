# Self-Hosted Sentry

[Sentry](https://sentry.io/), feature-complete and packaged up for low-volume deployments and proofs-of-concept.

Documentation [here](https://develop.sentry.dev/self-hosted/).
##
#https://help.clouding.io/hc/en-us/articles/13484335072924-How-to-Setup-Sentry-on-Ubuntu-22-04
#
Prerequisites
Ubuntu OS (20.04 or later recommended)
Docker and Docker Compose installed
At least 4 vCPUs and 8GB RAM (Recommended: 8 vCPUs, 16GB RAM)
in azure use -> B4als_v2, B4as_v2

A valid domain name (if you want to access Sentry via HTTPS)
SSL certificate (for secure access)
######
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl enable --now docker
#
sudo apt install -y git curl
#
#under ubuntu user 
sudo usermod -aG docker ubuntu
#
docker run hello-world
#
git clone https://github.com/getsentry/self-hosted.git ~/sentry
cd ~/sentry
#
#####
nano /home/ubuntu/sentry/sentry/sentry.conf.example.py
nano sentry/sentry.conf.py
# To uncomment and modify the line (enter your Sentry registration):
CSRF_TRUSTED_ORIGINS = ["https://sentry.example.com", "http://127.0.0.1:9000"]
CSRF_TRUSTED_ORIGINS = ["https://sentry.hubler.abc", "https://az-sentry.hubler.abc", "http://11.11.11.11:9000", "http://127.0.0.1:9000"]
#nginx
sudo apt update
sudo apt install -y nginx
##
ubuntu@sentry-self-hosted:~/sentry$ cat /etc/nginx/conf.d/sentry.conf
server {
    listen 80;
    server_name az-sentry.hubler.abc;

    # Redirect all HTTP traffic to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name az-sentry.hubler.dev;

    # SSL Configuration
    ssl_certificate /etc/nginx/ssl/hubler.dev.wc/fullchain.pem;
    ssl_certificate_key /etc/nginx/ssl/hubler.dev.wc/privkey.pem;

    # Recommended SSL settings
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    location / {
        proxy_pass http://127.0.0.1:9000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
ubuntu@sentry-self-hosted:~/sentry$

##





@
#Generate the Secret Key Manually Run the following command in your terminal:
docker run --rm getsentry/sentry:nightly config generate-secret-key
#inside nano .env add 
##
Status: Downloaded newer image for getsentry/sentry:nightly
)9gontl1uytzyip-03)a@psxhco!qj*-^)_4osz5_s76!%zzpv
ubuntu@devops:~/sentry$

##########
Step 4: Install Sentry
Run the installation script:

./install.sh

##
