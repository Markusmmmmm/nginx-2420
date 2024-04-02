First thing to do is update any system packages
```sudo pacman -Syu```
Then install vim and nginx
```sudo pacman -S vim```
```sudo pacman -S nginx```
Then download git
```sudo pacman -S git```
Create path /web/html/nginx-2420
```sudo -p mkdir /web/html/nginx-2420```
Then go to the nginx directory
```cd /etc/nginx```
Then create a config file for the nginx-2420 directory
```sudo vim nginx-2420.conf```
Then type in this code
```
server {
    listen 80;
    server_name localhost;

    root /web/html/nginx-2420;
    index index.html;
    location / {
        index index.html
    }
}
```
This code sets up a block that listens on port 80 and uses files from the /web/html/nginx-2420
Then start nginx using the code
```sudo systemctl start nginx```
Then enable nginx
```sudo systemctl enable nginx```
Then go back to the nginx-2420 directory 
```cd /web/html/nginx-2420```
Then create a test file called index.html
```sudo vim index.html```
copy and paste this code in there
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>
```
    
