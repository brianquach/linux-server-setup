# Linux Server Configuration

Website URL: [http://ec2-52-36-2-69.us-west-2.compute.amazonaws.com/][1]  
Public IP: 52.36.2.69  
Port: 2200

## Table of Contents

* [Software Summary](#Software-summary)
* [Configuration Summary](#configuration-summary)
* [Additional Features](#additional-features)
* [Resources Used](#resources-used)
* [Configurated By](#configurated-by)

## Software Summary

* [Book Catalog](https://github.com/brianquach/udacity-nano-fullstack-catalog): Book catalog web application.
* [Apache2](https://httpd.apache.org/): HTTP Web Server used host the book catalog web app.
* [Flask](http://flask.pocoo.org/): Web framework used by book catalog web app.
* [PostgreSQL](https://www.postgresql.org/): Back-end database for the book catalog web app.
* [Psycopg](http://initd.org/psycopg/): PostgreSQL adapter for Python.
* [Virtualenvs](http://docs.python-guide.org/en/latest/dev/virtualenvs/): Create isolated Python environment
* [Mod_wsgi](http://flask.pocoo.org/docs/0.11/deploying/mod_wsgi/): Tool used to server Python web applications.
* [PIP](https://pip.pypa.io/en/stable/quickstart/): Used to install listed depedencies in requirements.txt file for book catalog.
* [GIT](https://git-scm.com/): Distributed version souce control system.
* [Finger](http://www.unix.com/man-page/freebsd/1/finger/): User look-up utility.
* [Network Time Protocol](http://www.ntp.org/): Synchronizes time over a network.
* [Unattended-upgrades](https://help.ubuntu.com/lts/serverguide/automatic-updates.html): Automatic package and security updates.
* [Glances](https://nicolargo.github.io/glances/): Operating System monitoring tool.
* [Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page): Server security tool.

## Configuration Summary

## Additional Features

##### Unattended Upgrades
Unattended-upgrades automatically installs stable updated packages or security updates. Modifying update frequency and blacklisting specific packages can be done through editing the configuraiton files specified in [server guide][3]. After setup and configuration modifications the process is hands-off.

##### Fail2Ban
Fail2Ban scans logs and bans IP addresses deemed suspicious through unusual user activites (ie. too many password attempts). Various settings such as number of attempts to trigger suspicious activity, ban length times, and services to monitor can be configured in the `/etc/fail2ban/jail.local` config file. More configuration settings and explainations can be found in the [fail2ban wiki][5]. After modification fail2ban must be stopped and started again with the following commands:
```sh
sudo service fail2ban stop
sudo service fail2ban start
```

##### Glances
Glances helps monitor operating system by tracking the various resources (CPU, memory, process, etc) being used by the operating system and providing a real-time view to the user. Glances can be used by running the command `glances` in the terminal. For more information on Glances usages visit their [read the docs][4].

## Resources Used

- https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
- http://askubuntu.com/questions/365087/grant-a-user-permissions-on-www-data-owned-var-www
- http://stackoverflow.com/questions/31168606/internal-server-error-target-wsgi-script-cannot-be-loaded-as-python-module-and
- http://httpd.apache.org/docs/2.4/vhosts/
- http://flask.pocoo.org/docs/0.10/deploying/mod_wsgi/
- http://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNSTRING
- http://docs.sqlalchemy.org/en/latest/dialects/postgresql.html#module-sqlalchemy.dialects.postgresql.psycopg2
- https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2
- http://askubuntu.com/questions/9/how-do-i-enable-automatic-updates
- https://pypi.python.org/pypi/Glances
- http://askubuntu.com/questions/563931/cant-isntall-pysensors-sudo-pip-install-pysensors-generates-valueerror-us
- https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04

## Configurated By

Brian Quach
* <https://github.com/brianquach>

[1]: http://ec2-52-36-2-69.us-west-2.compute.amazonaws.com/ "Brian Quach Book Catalog Web App"
[2]: https://help.ubuntu.com/lts/serverguide/NTP.html "Ubuntu NTP Server Guide"
[3]: https://help.ubuntu.com/lts/serverguide/automatic-updates.html "Unattended Upgrades Server Guide"
[4]: http://glances.readthedocs.io/en/latest/ "Glances Read The Docs"
[5]: http://www.fail2ban.org/wiki/index.php/MANUAL_0_8 "Fail2ban Wiki"