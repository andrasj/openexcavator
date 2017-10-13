# openexcavator

## About
The application is intended to be used with a high precision GPS receiver for assisting excavation operations (assist with bucket positioning for land leveling, trenching).  
It is designed to run on a Raspberry Pi (but can run on other devices as well) and present a web interface used by the operator on a smartphone / tablet / notebook PC.

## Installation
Install dependencies:
```
pip install -r requirements.txt
```
Copy source files
```
git clone https://github.com/dkwiebe/openexcavator
```
Edit relevant entries in the settings.py file such as GPS host and port.  
To enable the application to start at boot copy the `openexcavator.service` systemd file from the `scripts` folder to `/etc/systemd/system` and enable it using:
```
systemctl daemon-reload  
systemctl enable georgina
systemctl start georgina
```
Check the logs to be sure the application is working as expected:
```
journalctl -f -u openexcavator
```
While not strictly necessary it's a good idea to put `nginx` in front of the web application:
```
sudo apt-get install nginx
```
Afterwards edit `/etc/nginx/sites-available/default`:
```
server {
        listen 80 default_server;

        location / {
                proxy_pass http://127.0.0.1:8000;
        }

}
```