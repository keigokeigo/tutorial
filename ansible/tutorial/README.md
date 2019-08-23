# これ、何？

* Ansible のチュートリアル。Docker環境ですべて完結。
* 以下のような構成
```
builder
   +--> node1
   +--> node2
```

# やり方

## on dockerhost

```
$ sudo docker-compose up -d

# コンテナログイン
$ sudo docker-compose exec --privileged builder /bin/bash
```

## on "builder" container

```
# -- dry-run 的な
# ansible-playbook --check --diff -i /playbook/testing /playbook/tutorial.yml

PLAY [tutorial] *******************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************
ok: [node2]
ok: [node1]

TASK [create directory] ***********************************************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/var/tmp/foo",
-    "state": "absent"
+    "state": "directory"
 }

changed: [node2]
--- before

(.......)

# -- 実行
# ansible-playbook -i /playbook/testing /playbook/tutorial.yml

# -- 実行（並列度=1）
# ansible-playbook -f 1 -i /playbook/testing /playbook/tutorial.yml
```

# 備考

## 内部的なSSHアカウントとそのPassword
* User=`user`
* Passwd=`newpass`

* `./start.sh を参照されたし。`