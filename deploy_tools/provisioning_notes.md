Provisioning new site
=====================


## Required packages:

* nginx
* Python 3.6
* Git
* pip
* virtualenv

* see nginx.template.conf
* replace SITENAME with, e.g., staging.my-domain.com


## Systemd service

* see gunicorn-systemd.template.service
* replace USERNAME with local account username and SITENAME with, e.g., staging.my-domain.com

sed "s/SITENAME/superlists.zfind.info/g" deploy_tools/nginx.template.conf | sed "s/USERNAME/tdduser/g" | sudo tee /etc/nginx/sites-available/superlists.zfind.info

sudo ln -s ../sites-available/superlists.zfind.info \
    /etc/nginx/sites-enabled/superlists.zfind.info

sed "s/SITENAME/superlists.zfind.info/g" deploy_tools/gunicorn-systemd.template.service | sed "s/USERNAME/tdduser/g" | sudo tee /etc/systemd/system/gunicorn-superlists.zfind.info.service


## Folder structure:
Assume we have a user account at /home/USERNAME

/home/USERNAME
└── sites
    └── SITENAME
         ├── database
         ├── source
         ├── static
         └── virtualenv