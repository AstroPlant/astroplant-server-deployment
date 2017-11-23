# AstroPlant deployment
AstroPlant server deployment using Ansible.

# Requirements
Ansible 2.3

# Configuring
You need to supply a secret key for the Django application and a password for the database user. Copy the files in `./conf` and remove the `.example` suffix, and edit the newly created files.

# Executing playbooks (on the Ansible controller machine)
Before executing playbooks, add your public SSH key to the target machines' authorized keys. Otherwise Ansible cannot connect.

Run the AstroPlant playbook to deploy the server:

```bash
ansible-playbook astroplant.yml
```

# Perform manually (on the back-end machine) 

Create/upgrade the database (make sure to backup the current database first):

```bash
source /home/astroplant/astro_venv/bin/activate && python manage.py migrate
```

If desired, you can import default AstroPlant data (such as measurement types, peripheral device definitions, etc.):

```bash
source /home/astroplant/astro_venv/bin/activate && python manage.py loaddata astroplant
```

Manually request a LetsEncrypt certificate for your domain:
```bash
$ /opt/certbot/certbot-auto certonly --webroot -w /var/www/astroplant -d example.com
```

Run a Daphne worker service
```bash
source /home/astroplant/astro_venv/bin/activate && python manage.py runworker
```

Start the Daphne server to serve request:
```bash
source /home/astroplant/astro_venv/bin/activate && daphne --ws-protocol "graphql-ws" --proxy-headers server.asgi:channel_layer
```
