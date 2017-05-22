# AstroPlant deployment
AstroPlant server deployment using Ansible.

# Requirements
Ansible 2.3

# Executing playbooks
Before executing playbooks, add your public SSH key to the target machines' authorized keys. Otherwise Ansible cannot connect.

```
ansible-playbook astroplant.yml
ansible-playbook astroplant.yml -l production
```

# Used roles:
Ferm role based on: https://github.com/nickjj/ansible-ferm
Fail2ban role based on: https://github.com/resmo/ansible-role-fail2ban
...


# Todo:
Edit `server/settings.py`

Manually run
```
source /home/astroplant/astro_venv/bin/activate
python manage.py collectstatic
```

Manually request letsencrypt certificate:
```
$ /opt/certbot/certbot-auto certonly --webroot -w /var/www/astroplant -d astroplant.kepow.org
```

To start the server:
```
uwsgi --ini uwsgi.ini
```
