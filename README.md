# Ansible PDM Mailserver

Master: [![Build Status](https://travis-ci.org/lobsterdore/ansible-pdm-mailserver.svg?branch=master)](https://travis-ci.org/lobsterdore/ansible-pdm-mailserver)
Develop: [![Build Status](https://travis-ci.org/lobsterdore/ansible-pdm-mailserver.svg?branch=develop)](https://travis-ci.org/lobsterdore/ansible-pdm-mailserver)

* [To install](#to-install)
* [How to use](#how-to-use)
* [Tags](#tags)
* [Development](#development)
* [Contributing](#contributing)

Install and configures Postfix, Dovecot and supporting packages, a complete all in one
mailserver based on [Sovereign](https://github.com/sovereign/sovereign).

In addition to installing and configuring software, this role can also configure
an EC2 instance with DNS entries and backup/restore from S3.





## To install

The easiest installation method is via Ansible Galaxy:

```BASH
ansible-galaxy install lobsterdore.ansible-pdm-mailserver
```

In requirements file:

```BASH
---
# requirements.yml

- src: lobsterdore.ansible-pdm-mailserver
  version: v1.0.0

```

To see available versions please check this roles [Ansible Galaxy page](https://galaxy.ansible.com/lobsterdore/ansible-pdm-mailserver/).




## How to use

Example setup:

```YAML
---

dependencies:

  - role: ansible-pdm-mailserver
    ansible_pdm_mailserver_aws_r53_zone: somehost.io
    ansible_pdm_mailserver_aws_s3_backup_bucket: bucket.mail.somehost.io
    ansible_pdm_mailserver_aws_s3_backup_bucket_enable_dkim_keys: yes
    ansible_pdm_mailserver_db_admin_password: password
    ansible_pdm_mailserver_db_admin_username: root
    ansible_pdm_mailserver_db_database: mailserver
    ansible_pdm_mailserver_db_username: mailserver
    ansible_pdm_mailserver_db_opendmarc_database: mailserver_opendmarc
    ansible_pdm_mailserver_domain: somehost.io
    ansible_pdm_mailserver_main_user_name: someuser
    ansible_pdm_mailserver_virtual_users:
      - account: someuser
        domain: somehost.io
        password_hash: "$6$Zz50hoe2bM3DNiCO$S8Kfxw/WHhWeUROzfvZ0rn8FXiPSiRCoV0oHQFMizzE5ugUk4xufBb0K/t5oCEMs4AE8XySywmGpXRF3/UlWA1"
        domain_pk_id: 1

```




## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs packages, can be used to bake AMIs
* `configure` - Configures packages, can be used on boot for pre-baked AMIs




## Development

A Vagrant box is included that you can use to test this role, a Makefile is included as well
that contains some useful targets for testing, to see a list of targets you can do the following:

```BASH
make
```




## Contributing

If you would like to contribute to this role please open a Github issue first, then open your PR and reference the issue.
