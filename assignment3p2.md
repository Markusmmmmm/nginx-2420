Install ufw
```sudo pacman -Syu ufw```
Start and enable ufw
```sudo systemctl start ufw.service```
```sudo systemctl enable ufw.service```
Check the status of ufw to see if its enabled 
```ufw status```
Configure ufw to deny and allow 
```sudo ufw default deny incoming```
```sudo ufw default allow outgoing```
Then allow http and https
```sudo ufw allow http```
```sudo ufw allow https```
Download the hello-service file into your downloads directory
then go into sftp 
```sftp -i .ssh/DO-key marku@64.23.129.51```
Now download it
```put C:\Users\your-name\Downloads\hello-server```
Go back into your droplet and move the backend to the bin 
```sudo mv hello-server /usr/local/bin```
Then create a new service file for the backend
```sudo vim /etc/systemd/system/backend.service```
copy this in
[Unit]
Description=Backend Service
After=network.target

[Service]
ExecStart=/usr/local/bin/backend
Restart=always

[Install]
WantedBy=multi-user.target

Then enable and start the service
```sudo systemctl enable backend```
```sudo systemctl start backend```
then create a block config file for the backend
```sudo vim /etc/nginx/sites-available/backend```
copy this in
server {
    listen 80;
    server_name your_domain_or_IP;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

create a symbolic link to the sites enabled directory
```sudo ln -s /etc/nginx/sites-available/backend /etc/nginx/sites-enabled```
Then test and reload nginx
```sudo nginx-t```
```sudo systemctl reload nginx```
Enable ufw 
```sudo ufw enable```
Go into postamn and type
```curl http://your_domain_or_IP/hey```
```curl -X POST -H "Content-Type: application/json" -d '{"message": "Hello from your server"}' http://your_domain_or_IP/echo```


You have now set up a reverse proxy with Nginx and configured a firewall using ufw