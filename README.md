# ansible-role-pam

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-pam.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-pam)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-pam-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/pam)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Pluggable Authentication Modules

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    pam_limits_conf: []
    pam_limits_d: []
    pam_pwquality_dcredit: 1
    pam_pwquality_difok: 5
    pam_pwquality_gecoscheck: 0
    pam_pwquality_lcredit: 1
    pam_pwquality_maxrepeat: 0
    pam_pwquality_maxclassrepeat: 0
    pam_pwquality_minclass: 0
    pam_pwquality_minlen: 9
    pam_pwquality_ocredit: 1
    pam_pwquality_ucredit: 1

Below is example syntax for each variable:

    pam_limits_conf:
      - domain: joe
        limit_item: nofile
        limit_type: soft
        value: 64000
      - domain: smith
        limit_item: fsize
        limit_type: hard
        value: 1000000

    pam_limits_d:
      - file: ansible
        order: 99
        limits:
          - domain: joe
            limit_item: nofile
            limit_type: soft
            value: 64000
          - domain: smith
            limit_item: fsize
            limit_type: hard
            value: 1000000

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.pam
          pam_limits_d:
            - file: linuxhq
              order: 99
              limits:
                - domain: '*'
                  limit_item: core
                  limit_type: hard
                  value: 0
          pam_pwquality_dcredit: -1
          pam_pwquality_difok: 8
          pam_pwquality_gecoscheck: 1
          pam_pwquality_lcredit: -1
          pam_pwquality_maxrepeat: 4
          pam_pwquality_maxclassrepeat: 4
          pam_pwquality_minclass: 4
          pam_pwquality_minlen: 15
          pam_pwquality_ocredit: -1
          pam_pwquality_ucredit: -1

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
