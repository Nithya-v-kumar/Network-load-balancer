Setup 2 private & 2 public subnet with one Pulic RT & one Private RT
VPC-11.0.0.0/16
subnet-public1-11.0.1.0/24
subnet-public2-11.0.2.0/24
subnet-private-11.0.3.0/24
subnet-private-11.0.4.0/24

## Install Apache

```
#!/bin/bash

# Update package lists
yes | sudo apt update

# Install Apache2
yes | sudo apt install apache2

# Write a basic HTML page with hostname and IP
sudo bash -c 'cat <<EOF > /var/www/html/index.html
<h1>Server Details</h1>
<p><strong>Hostname:</strong> $(hostname)</p>
<p><strong>IP Address:</strong> $(hostname -I | cut -d" " -f1)</p>
EOF'

# Restart Apache to ensure it's running
sudo systemctl restart apache2
```
setting up custom images for Apache one is foo & another is bar in order to get difference bet Application & Network LB
## Command for creating `foo`,  `bar` pages

```
sudo mkdir /var/www/html/foo
sudo mkdir /var/www/html/bar

sudo touch /var/www/html/foo/index.html
sudo touch /var/www/html/bar/index.html

sudo vi /var/www/html/foo/index.html
<h1>Hello from /foo demo-nlb-ec2-1</h1><p>This is a sample hello message in /foo.html.
sudo vi /var/www/html/bar/index.html
<h1>Hello from /bar demo-nlb-ec2-1</h1><p>This is a sample hello message in /bar.html.</p>"

sudo systemctl daemon-reload
sudo systemctl restart apache2
```
run in browser http://public IP/foo/
run in browser http://public IP/bar/

the difference in application & network we can access bar & foo with 2 target group configuration in application LB & network LB we cannot

