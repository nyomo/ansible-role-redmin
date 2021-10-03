Redmine
=========

AnsibleでCentOS7にRedmineをインストールするRole

Requirements
------------

CentOS7用

動作確認にmoleculeとDockerを使って居る

Role Variables
--------------

- redmine_db_password redmine用データベースのパスワード
- tenants redmineのインストールディレクトリ名とホスト名。配列で複数のredmineをインストール出来る
  * name ディレクトリ名とデータベース名とデータベースのユーザ名に利用される
  * hostname　ホスト名(今の所未使用)

更に依存関係のあるrole用に以下の設定を行う必要がある

- nyomo.rbenv用
  * rbenv_dir rbenvのインストール先
  * ruby_version 利用するrubyのバージョン
- nyomo.mysql57用
  * mysql_root_password mysqlのrootパスワード
[MySQL5.7標準のパスワードポリシー](https://dev.mysql.com/doc/refman/5.7/en/validate-password-options-variables.html)によると、8文字以上で数字大文字小文字記号が含まれて居る必要がある

vars/main.ymlの例

```
rbenv_dir: /opt/rbenv
ruby_version: "2.7.4"
mysql_root_password: "test!Pass1"
redmine_db_password: "test!Pass2"
tenants:
- name: redmine1
  hostname: hoge.test.com
- name: redmine2
  hostname: fuga.test.com
```

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

1. `ansible-galaxy install -r requirements.yml`
2. playbook main.yml
```
- hosts: all
  vars_files: 
  - vars/main.yml
  pre_tasks:
  - name: update packages
    yum:
      update_cache: yes
    changed_when: no
  roles:
  - nyomo.redmine
```

License
-------

Apache-2.0

Author Information
------------------

https://github.com/nyomo/
