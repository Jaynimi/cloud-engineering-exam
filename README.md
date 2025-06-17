# Dynamic Startup Landing Page

This project showcases a deployment of a dynamic landing page using Nginx.

## 🛠️ Tech Stack
- Ubuntu 24.04.2 LTS (AWS EC2)
- Nginx (Reverse Proxy)
- TailwindCSS
- Node.js and Express

## 🚀 Setup Steps
1. Provision EC2 Ubuntu server
. Log into AWS Console
Visit: https://console.aws.amazon.com
Sign in with your AWS credentials.

. Launch a New Instance

. Launch the Instance

. Connect to Your EC2 Instance
Go to Instances in EC2 dashboard.

To install webserver
update the library

2. Install Node.js & Nginx
##
        sudo apt install nginx -y
        curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
        sudo apt install -y nodejs

3. Deploy `index.html` and `server.js`

##
        npm init -y
        npm install express
        node server.js

4. Configure Nginx reverse proxy
##
        sudo nano /etc/nginx/sites-available/myapp


5. Save the Nginx and the server.js configuration files

##
        server {
            listen 80;
            server_name localhost;
            
            location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                }
        }

##
    const express = require('express');
    const path = require('path');

    const app = express();
    const PORT = 3000;

    // Serve static files
    app.use(express.static(path.join(__dirname, 'public')));

    // Start the server
    app.listen(PORT, '0.0.0.0', () => {
    	console.log(`Node server is running at 
    			http://localhost/
    			:${PORT}`);
    }); 





6. Enable the config:

##
        sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
        sudo nginx -t
        sudo systemctl restart nginx

## 🌍 Live Demo
Public IP: http://18.203.84.96:3000/

## 📸 Screenshot
![Screenshot](<Screenshot 2025-06-17 213819.png>)