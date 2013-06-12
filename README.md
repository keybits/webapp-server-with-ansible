# Web application server with Ansible

**NB This is a work in progress. Use at your own risk.**

The setup here has not been tested. Please don't base your production server on this code without testing and checking security. Additions and pull requests for enhancements gratefully received!

## Aim

Provision an Ubuntu 12.04 64bit Server for serving web applications with the following stack:

- Python
- Flask
- uWSGI
- NGINX
- Postgresql
- Node (to be completed)

The scripts should work with small modifications on other version of Ubuntu and Debian.

## Getting started

### Development box

1. Install Ansible

### Server

1. Set up a VPS with a bare Ubuntu 12.04 64bit image.
2. Make sure you can log into the server from your development box using key based login and a non root account with sudo priviliges.

#### Firewall setup

*TODO: The following needs to be added to the server setup playbook.*

Set up the firewall on the server with:

```
ufw default deny incoming
ufw default allow outgoing
ufw allow www
ufw allow ssh
ufw allow ntp
ufw enable
```

Make sure you can still log in before clossing the SSH session.

## Provisioning

1. Make a `hosts` file in the `devops` folder based on `hosts.example`
2. Update the `hosts` and `user` information in `setupserver.yml`, `setup-database.yml` and `deploy.yml` to your own values.
2. Run `ansible-playbook devops/setup-server.yml -i devops/hosts --ask-sudo-pass`
3. Enter password for your user on the server
4. Create and test database with: `ansible-playbook devops/setup-database.yml -i devops/hosts --ask-sudo-pass`

## Deployment

1. Run `ansible-playbook devops/deploy.yml -i devops/hosts --ask-sudo-pass`

This will set up a basic Flask application to run via Supervisor using uWSGI and Nginx.

2. Visit `http://[yourhost]` and you should see the application running.



## Using the