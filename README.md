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



