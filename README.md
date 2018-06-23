# ansible-role-logrotate

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-logrotate.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-logrotate)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-logrotate-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/logrotate)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Rotates, compresses, and mails system logs

## Requirements

None

## Role Variables

Available variables are listed below, along with default values.

    logrotate:
      compress: false
      create: true
      dateext: true
      include: /etc/logrotate.d
      rotate: 4
      weekly: true
    logrotate_d: []
    logrotate_files:
      - files:
          - /var/log/btmp
        options:
          create: '0600 root utmp'
          missingok: true
          monthly: true
          rotate: 1
      - files:
          - /var/log/wtmp
        options:
          create: '0664 root utmp'
          minsize: 1M
          monthly: true
          rotate: 1
    logrotate_rwtab:
      dirs:
        - /var/lib/logrotate

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.logrotate
          logrotate:
            compress: true
            create: true
            daily: true
            dateext: true
            include: /etc/logrotate.d
            rotate: 1
            shred: true
          logrotate_d:
            - name: linuxhq
              files:
                - /var/log/linuxhq.log
              options:
                compress: true
                dateext: true
                rotate: 1

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
