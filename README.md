# ansible-role-pam

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-pam.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-pam)

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

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
