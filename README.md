# ansible-letsencrypt

An easy way to setup enable https with Letsencrypt certificate.

Up to 3 services in one run using `X_DOMAIN_NAME` and `PROXY_PORT_X` variables.

## How to use it ?

### Install ansible:

On Ubuntu
```
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
```

### Modify hosts:
First do this: `cp hosts.tpl hosts`

Modify the `hosts` file by removing `ubuntu@XXX.XXX.XXX.XXX` and adding the address hostname@address of your server. (same as ssh host)

/!\ Don't forget to add your public ssh key to your server `~/.ssh/authorized_keys`

### Choose target port and domaine name
First  do this: `cp -r group_vars_tpl group_vars` 

Modify `group_vars/nginx-letsencrypt.yml` with the your email, domain names `X_DOMAIN_NAME` and ports forwarding `PROXY_PORT_X` (using nginx)

If you don't want to enable the 3 domains, you may just comment the line `X_DOMAIN_NAME` that you don't want to activate with a # at the beginning of the line.

You may need to remove existing nginx configuration file using port `443` from `/etc/nginx/sites-enabled/`

### Start ansible:

Use the following command to start script:

`ansible-playbook -i hosts site.yml -K` (the -K is not mandatory, use it only if sudo have a password)

You will need to provide sudo password of your host.

And Voilà!
