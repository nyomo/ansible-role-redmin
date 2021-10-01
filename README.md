Redmine
=========

AnsibleでCentOS7にRedmineをインストールするRole 建設予定地

Requirements
------------

CentOS7用

動作確認にmoleculeとDockerを使って居る

Role Variables
--------------

未定

Dependencies
------------

- nyomo.mysql57
MySQL5.7が動作して居れば良い
- nyomo.rbenv
rootユーザがruby2.7.4とgemをつかえる状態になって居れば良い
- nyomo.apache_passenger
apacheとpassengerが動いて居る必要がある。

Example Playbook
----------------

1. requiement.yml
```
- name: nyomo.mysql57
  src: https://github.com/nyomo/ansible-role-mysql57.git
- name: nyomo.rbenv
  src: https://github.com/nyomo/ansible-role-rbenv.git
- name: nyomo.apache_passsenger
  src: https://github.com/nyomo/ansible-role-apache_passenger.git
```
2. `ansible-galaxy install -r requirements.yml`
3. playbook
```
---
- hosts: all
  roles:
  - nyomo.redmine
```

License
-------

Apache-2.0

Author Information
------------------

https://github.com/nyomo/
