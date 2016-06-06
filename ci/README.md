## CI setup based on drone

This allows to easily setup a [drone.io](https://drone.io) instance on a server via [ansible](https://www.ansible.com/).

### Required configuration

Create a file `hosts` with following content:

```
[ci]
IP ansible_ssh_user=USER_NAME ansible_become_pass=USER_PASSWORD github_client_id=ID github_client_secret=SECRET
```

 * **IP** - IP address of the server
 * **USER_NAME** - ssh user name for this server
 * **USER_PASSWORD** - ssh user password for use with `sudo`
 * **ID** - client ID from GitHub ([generate personal](https://github.com/settings/applications/new) or [generate organisation](https://github.com/organizations/ORGANISATION/settings/applications/new))
 * **SECRET** - client secret from GitHub (see previous item)

### Optional configuration

At the beginning of the `playbook.yml` there are configuration variables to make it easy to update key parameter of the instance.

 * `registration_open` - set this to `true` to allow users to register at this drone instance (default: `false`)
 * `limit_to_organisation` - this limits the repositories that could be enabled on this instance to an GitHub organisation (default: `nextcloud`)
 * `drone_version` - the used docker version of the image `drone/drone`

### Deploy this

```
# install ansible (e.g. via pip install ansible into a virtual env)
$ ansible-playbook -i hosts playbook.yml
```
