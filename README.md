# Linux Server Configuration
This is a how-to guide on how to configure a baseline Amazon Web Service Ubuntu server into a full-fledged Apache web host that serves the [book catalog web app](https://github.com/brianquach/book-catalog).  

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
* [PHP](http://php.net): PHP installed for third-party application dependencies.
* [GIT](https://git-scm.com/): Distributed version souce control system.
* [Finger](http://www.unix.com/man-page/freebsd/1/finger/): User look-up utility.
* [Network Time Protocol](http://www.ntp.org/): Synchronizes time over a network.
* [Unattended-upgrades](https://help.ubuntu.com/lts/serverguide/automatic-updates.html): Automatic package and security updates.
* [Glances](https://nicolargo.github.io/glances/): Operating System monitoring tool.
* [Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page): Server security tool.

## Configuration Summary

1. Update and upgrade current packages.
2. Change **SSH** port to 2200.
3. Set **UFW** to allow only ports 2200, 80, and 123.
4. Create user **grader**, set a strong password, and give sudo access rights by using `visudo`.
5. Setup **SSH** for user grader.
6. Disable Root login.
7. Add line `127.0.1.1 ip-10-20-33-99` to `/etc/hosts` to solve sudo error for grader.
8. Timezone already set to UTC; check using `date` or `date +%Z`.
9. Install **NTP** and enable time-synchronization with **timedatectl**.
10. Install **Apache2**, **PostgreSQL**, **Flask**, and **mod_wsgi**.
11. Install **git** to clone book catalog repository.
12. Install PIP and run `pip install -r requirements.txt`
13. Switch user to **postgres**, and create **catalog_access_role** with CreateDB and No login access rights in **psql**.
14. Create **catalog_db** with **catalog_access_role** as owner.
15. Create user **catalog** and grant **catalog_access_role** to **catalog**.
16. Run `python create_db` to initialize application database.
17. Install **virtualenvs** and create virtual environment for catalog web app.
18. Add **catalog.wsgi** to catalog web app.
19. Add vhost configuration for book catalog web app.
20. Update catalog application code to use database connection string: `postgresql://catalog@localhost/catalog_db`.
21. Update catalog application code to use absolute paths instead of relative paths (mod_wsgit requirement).
22. Update javascript to redirect to correct url (ie. replace localhost:8080 with AC2 url http://ec2-52-36-2-69.us-west-2.compute.amazonaws.com/) for **OAuth**.
23. Create new group called **catalog_site** and give R,W,X permission as group owner to `/var/www/catalog`.
24. Add user **www-data** to **catalog_site** group.
25. Add [additional features](#additional-features).

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