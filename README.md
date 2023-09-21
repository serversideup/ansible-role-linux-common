<p align="center">
		<a href="https://github.com/serversideup/ansible-linux-common"><img src="https://raw.githubusercontent.com/serversideup/ansible-linux-common/main/.github/img/header.png" width="1280" alt="GitHub Header"></a>
</p>
<p align="center">
	<a href="https://github.com/serversideup/ansible-linux-common/actions/workflows/publish_docker-images-production.yml"><img alt="Build Status" src="https://img.shields.io/github/actions/workflow/status/serversideup/ansible-linux-common/release.yml"></a>
	<a href="https://github.com/serversideup/ansible-linux-common/blob/main/LICENSE" target="_blank"><img src="https://badgen.net/github/license/serversideup/ansible-linux-common" alt="License"></a>
	<a href="https://github.com/sponsors/serversideup"><img src="https://badgen.net/badge/icon/Support%20Us?label=GitHub%20Sponsors&color=orange" alt="Support us"></a>
  <br />
  <a href="https://community.serversideup.net"><img alt="Discourse users" src="https://img.shields.io/discourse/users?color=blue&server=https%3A%2F%2Fcommunity.serversideup.net"></a>
  <a href="https://serversideup.net/discord"><img alt="Discord" src="https://img.shields.io/discord/910287105714954251?color=blueviolet"></a>
</p>

Hi! We're [Dan](https://twitter.com/danpastori) and [Jay](https://twitter.com/jaydrogers). We're a two person team with a passion for open source products. We created [Server Side Up](https://serversideup.net) to help share what we learn.

### Find us at:

* 📖 [Blog](https://serversideup.net) - get the latest guides and free courses on all things web/mobile development.
* 🙋 [Community](https://community.serversideup.net) - get friendly help from our community members.
* 🤵‍♂️ [Get Professional Help](https://serversideup.net/get-help) - get guaranteed responses within next business day.
* 💻 [GitHub](https://github.com/serversideup) - check out our other open source projects
* 📫 [Newsletter](https://serversideup.net/subscribe) - skip the algorithms and get quality content right to your inbox
* 🐥 [Twitter](https://twitter.com/serversideup) - you can also follow [Dan](https://twitter.com/danpastori) and [Jay](https://twitter.com/jaydrogers)
* ❤️ [Sponsor Us](https://github.com/sponsors/serversideup) - please consider sponsoring us so we can create more helpful resources

### Our Sponsors
All of our software is free an open to the world. None of this can be brought to you without the financial backing of our sponsors.

<p align="center"><a href="https://github.com/sponsors/serversideup"><img src="https://521public.s3.amazonaws.com/serversideup/sponsors/sponsor-box.png" alt="Sponsors"></a></p>

#### Individual Supporters
<!-- supporters --><a href="https://github.com/deligoez"><img src="https://github.com/deligoez.png" width="40px" alt="deligoez" /></a>&nbsp;&nbsp;<a href="https://github.com/alexjustesen"><img src="https://github.com/alexjustesen.png" width="40px" alt="alexjustesen" /></a>&nbsp;&nbsp;<a href="https://github.com/jeremykenedy"><img src="https://github.com/jeremykenedy.png" width="40px" alt="jeremykenedy" /></a>&nbsp;&nbsp;<!-- supporters -->

Linux Common
=========

 A simple playbook to secure your server, prep your users, and prepare your server for other uses. 

Requirements
------------

For now, this project focuses on supporting **Ubuntu 22.04** only. Choose any host that you'd like. All this role needs is an SSH connection to a user that has `sudo` privileges.

Role Variables
--------------

You can find all variables organized and documented in `defaults/main.yml`. Feel free to override any variable of your choice.

```yml
---
###########################################
# Basic Server Configuration
###########################################
server_timezone: "Etc/UTC"
server_contact: changeme@example.com

# SSH
server_ssh_port: "22"

## Email Notifications
postfix_hostname: "{{ inventory_hostname }}"

## Set variables below to enable external SMTP relay
# postfix_relayhost: "smtp.example.com"
# postfix_relayhost_port: "587"
# postfix_relayhost_username: "myusername"
# postfix_relayhost_password: "mysupersecretpassword"

###########################################
# APT Configuration
###########################################

# Time is in seconds (default: 24 hours)
apt_cache_expiration: 86400

# Common packages to install
common_installed_packages:
  - cron
  - curl
  - figlet
  - fail2ban
  - git
  - htop
  - logrotate
  - mailutils
  - ncdu
  - ntp
  - python3-minimal
  - ssh
  - tzdata
  - ufw
  - unattended-upgrades
  - unzip
  - wget
  - zip

# APT - Automatic Update Configuration
apt_periodic_update_package_lists: "1"
apt_periodic_download_upgradeable_packages: "1"
apt_periodic_autoclean_interval: "7"
apt_periodic_unattended_upgrade: "1"

###########################################
# Fun Terminal Customizations
###########################################
motd_header_text: "ServerSideUp"
motd_header_text_color: '\e[38;5;255m'
motd_header_background_color: '\e[48;5;34m'
motd_hostname_text_color: '\e[38;5;202m'
motd_services:
  - ufw
  - fail2ban
  - postfix

##############################################################
# Users
##############################################################

### Use the template below to set users and their authorized keys
## Passwords must be set with an encrypted hash. To do this, see the Ansible FAQ
## https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module

# users:
#   - username: alice
#     name: Alice Smith
#     state: present
#     groups: ['adm','sudo']
#     password: "$6$mysecretsalt$qJbapG68nyRab3gxvKWPUcs2g3t0oMHSHMnSKecYNpSi3CuZm.GbBqXO8BE6EI6P1JUefhA0qvD7b5LSh./PU1"
#     shell: "/bin/bash"
#     authorized_keys:
#       - public_key: "ssh-ed25519 AAAAC3NzaC1lmyfakeublickeyMVIzwQXBzxxD9b8Erd1FKVvu alice"

#   - username: bob
#     name: Bob Smith
#     state: present
#     password: "$6$mysecretsalt$qJbapG68nyRab3gxvKWPUcs2g3t0oMHSHMnSKecYNpSi3CuZm.GbBqXO8BE6EI6P1JUefhA0qvD7b5LSh./PU1"
#     groups: ['adm','sudo']
#     shell: "/bin/bash"
#     authorized_keys:
#       - public_key: "ssh-ed25519 AAAAC3NzaC1anotherfakekeyIMVIzwQXBzxxD9b8Erd1FKVvu bob"

### Additional users
## You can also set additional users (great if you're working with contractors or clients on certain groups of servers)
## These users will be flattened into the users list (if you set any settings below)

# additional_users:
#   - username: charlie
#     name: Charlie Smith
#     state: present
#     groups: ['adm','sudo']
#     password: "$6$mysecretsalt$qJbapG68nyRab3gxvKWPUcs2g3t0oMHSHMnSKecYNpSi3CuZm.GbBqXO8BE6EI6P1JUefhA0qvD7b5LSh./PU1"
#     shell: "/bin/bash"
#     authorized_keys:
#       - public_key: "ssh-ed25519 AAAAC3NzaC1lmyfakeublickeyMVIzwQXBzxxD9b8Erd1FKVvu alice"

#   - username: dana
#     name: Dana Smith
#     state: present
#     password: "$6$mysecretsalt$qJbapG68nyRab3gxvKWPUcs2g3t0oMHSHMnSKecYNpSi3CuZm.GbBqXO8BE6EI6P1JUefhA0qvD7b5LSh./PU1"
#     groups: ['adm','sudo']
#     shell: "/bin/bash"
#     authorized_keys:
#       - public_key: "ssh-ed25519 AAAAC3NzaC1anotherfakekeyIMVIzwQXBzxxD9b8Erd1FKVvu bob"
```

Dependencies
------------
See (`requirements.yml`)[./requirements.yml] for all collection dependencies.

To install all dependencies, run:

```bash
ansible-galaxy install -r requirements.yml
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: serversideup.linux_common, server_timezone: 'America/Chicago' }
