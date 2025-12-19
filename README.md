installed node

Create:
mkdir ~/node-backend && cd ~/node-backend
vi server.js

Added:
const http = require('http');
http.createServer((req, res) => {
  res.end('Hello from Node.js backend!');
}).listen(3000);

Run:
node server.js

##########################

For Reverse Proxy

paste this in sites available: 
location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}

<img width="409" height="114" alt="image" src="https://github.com/user-attachments/assets/9f16d893-4ac2-40bd-a4e2-75e515165361" />

Edit:

sudo nano /etc/nginx/sites-available/default
Replace contents with:

upstream backend_app {
    server 127.0.0.1:3001;
    server 127.0.0.1:3002;
}

server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://backend_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Run both servers
node server1.js &
node server2.js &

Reload NGINX
sudo nginx -t
sudo systemctl reload nginx


############# SSL/TLS #################

sudo openssl req -x509 -nodes -days 365 \
 -newkey rsa:2048 \
 -keyout /etc/ssl/private/nginx-selfsigned.key \
 -out /etc/ssl/certs/nginx-selfsigned.crt




 ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;




