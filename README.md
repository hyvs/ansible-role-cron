Ansible Role - Cron
===================

A Cron role to add cron jobs on elao symfony standard vagrant box


Requirements
------------

This role only run on elao symfony standard vagrant box. See https://vagrantcloud.com/elao/symfony-standard-debian


Role Handlers
-------------

cron restart


Role Variables
--------------

 Variable | Required | Default  | Choices        | Comments
 -------- | -------- | -------- | -------------- | --------------------------
 name     | yes      |          |                | Description of crontab entry. Must be unique.
 job      | *        |          |                | The command to execute. Required if state=present
 state    | no       | present  | present,absent | Whether to ensure the job is present or absent.
 day      | no       | *        |                | Day of the month the job should run (1-31, *, */2, etc)
 hour     | no       | *        |                | Hour when the job should run (0-23, *, */2, etc)
 minute   | no       | *        |                | Minute when the job should run (0-59, *, */2, etc)
 month    | no       | *        |                | Month of the year the job should run (1-12, *, */2, etc)
 weekday  | no       | *        |                | Day of the week that the job should run (0-6 for Sunday-Saturday, *, etc)

```yml
# Ensure a job that runs at 2 and 5 exists.
# Creates an entry like "0 5,2 * * ls -alh > /dev/null"
elao_cron: name="check dirs" minute="0" hour="5,2" job="ls -alh > /dev/null"

# Ensure an old job is no longer present. Removes any job that is prefixed
# by "#Ansible: an old job" from the crontab
elao_cron: name="an old job" state=absent
```

Example Playbook
----------------

- hosts: servers
roles:
- { role: elao.cron }


License
-------

MIT


Author Information
------------------

http://www.elao.com/
