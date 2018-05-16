pyslackers.python
=========

[![Build Status](https://travis-ci.org/pyslackers/ansible-role-python.svg?branch=master)](https://travis-ci.org/pyslackers/ansible-role-python)

Python role for ansible. This supports multiple python versions thanks to pythonz.

Role Variables
--------------

* `python_versions`: List of valid python versions to install.
* `virtualenvs`: Dict of virtual environment to create.
    * `path`: Virtual environment directory.
    * `version`: Virtual environment python version.
    * `requirements`: Requirements.txt file to install.
    * `pip_version`: Virtual environment pip version (default to `latest`).
    * `setuptools_version`: Virtual environment setuptools version (default to `latest`).
* `pythonz_repo`: Git url to the pythonz repository (default to `https://github.com/saghul/pythonz.git`).
* `pythonz_version`: Version of pythonz to download (default to `master`).
* `pip_version`: Pythonz pythons interpreter pip version (default to `latest`).
* `setuptools_version`: Pythonz pythons interpreter setuptools version (default to `latest`).

Example Playbook
----------------

```yml
- role: pyslackers.python
  python_versions:
    - "3.6.2"
    - "3.6.3"
  virtualenvs:
    env_1:
      path: /opt/env_1
      version: "3.6.1"
      requirements: requirements.txt
    env_2:
      path: /opt/env_2
      version: "3.6.2"
      pip_version: "8.0.1"
```

License
-------

MIT
