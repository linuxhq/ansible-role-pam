# ansible-role-pam

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-pam.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-pam)

RHEL/CentOS - Pluggable Authentication Modules

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    pam_limits_conf: []
    pam_limits_d: []

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

## License

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
