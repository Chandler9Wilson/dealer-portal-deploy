# Dealer Portal Deploy Instructions

---

Deploy instructions for the [dealer portal project](https://github.com/Chandler9Wilson/dealer-portal)

## Access

* SSH with `$ ssh guest@epoch0.chandler9wilson.com -p 2200 -i path/to/the/private_key`
  * Subdomain: epoch0.chandler9wilson.com
  * IP of the server: 104.131.165.145
  * SSH port: 2200
* You can view the project in a browser at http://epoch0.chandler9wilson.com

## Configuration

* Changes made to /etc/ssh/sshd_config
  * Port 2200
  * PermitRootLogin no
  * PasswordAuthentication no
* UFW config
  * Allow port 2200 tcp for alternate SSH port
    * `$ sudo ufw allow 2200/tcp`
  * Allow port 80 tcp for apache
    * `$ sudo ufw allow www`
  * Allow port 123 for NTP
    * `$ sudo ufw allow ntp`

## Installed Software

* apache
  * `$ sudo apt-get install apache2`
  * `$ sudo apt-get install apache2-dev`
* python3-dev
  * `$ sudo apt-get install python3-dev`
* All software installed during dealer portal setup script
  * postgresql
  * python3-venv
  * Python packages in requirements.txt
* Install mod_wsgi
  * From the project root `$ source env/bin/activate`
  * `$ pip install mod_wsgi`
* Install nvm
  * `$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash`
* Install node (after session restart)
  * `$ nvm install 8`

## Setting up the server

* Run `$ mkdir mod_wsgi-express-80` from your user's home directory
* Run below but update `chandler` to your user name
```bash
  mod_wsgi-express setup-server wsgi_server.py --port=80 --user www-data --group www-data --server-root=/home/chandler/mod_wsgi-express-80
```
* Make sure the default apache is not running by running `$ sudo service apache2 stop`
* Start with `$ /home/chandler/mod_wsgi-express-80/apachectl start`

## Accounts

* grader
  * password: n56ixBO6mj3q

## Guides Used

* relevant man pages
* Used [this](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04) for usermod command and the ssh-copy-id script. I have set up servers before just couldnt remember those two lines.
* A nice walk through the [options with UFW](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04) a little nicer/more concise than the man page.
* I am using the mod_wsgi-express script included with the [mod_wsgi package](https://pypi.python.org/pypi/mod_wsgi)