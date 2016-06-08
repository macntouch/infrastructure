## Installs LetsEncrypt.sh for easy cert retrieval

This allows to easily setup a [letsencrypt.sh](https://github.com/lukas2511/letsencrypt.sh) on a server to retrieve LetsEncrypt certs.

### Required configuration

Create a file `hosts` with following content:

```
[letsencrypt]
IP ansible_ssh_user=USER_NAME ansible_become_pass=USER_PASSWORD contact_email=EMAIL
```

 * **IP** - IP address of the server
 * **USER_NAME** - ssh user name for this server
 * **USER_PASSWORD** - ssh user password for use with `sudo`
 * **EMAIL** - email address to register with at LetsEncrypt

### Deploy this

```
# install ansible (e.g. via pip install ansible into a virtual env)
$ ansible-playbook -i hosts playbook.yml
```

### Add new domains

Add a new line with the domain to `/etc/letsencrypt.sh/domains.txt` and then run `/opt/letsencrypt/letsencrypt -c` to get the certificates. The certificates are placed in the folder `/etc/letsencrypt.sh/certs/`.
