# AstroPlant deployment
AstroPlant server deployment using Ansible.

# Requirements
Ansible 2.3

# Configuring
You need to supply a secret key for the Django application and a password for the database user. Copy the files in `./conf` and remove the `.example` suffix, and edit the newly created files.

# Executing playbooks
Before executing playbooks, add your public SSH key to the target machines' authorized keys. Otherwise Ansible cannot connect.

Run the AstroPlant playbook to deploy the server:

```
ansible-playbook astroplant.yml
```

# Manual 

Create/upgrade the database (make sure to backup the current database first):

```
source /home/astroplant/astro_venv/bin/activate && python manage.py migrate
```

Manually request letsencrypt certificate:
```
$ /opt/certbot/certbot-auto certonly --webroot -w /var/www/astroplant -d astroplant.kepow.org -d astroplant.io
```

Start the server:
```
source /home/astroplant/astro_venv/bin/activate && uwsgi --ini ~/uwsgi.ini
```
