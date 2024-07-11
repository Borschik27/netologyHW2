0Домашнее задание к занятию 5. «Практическое применение Docker»

Dockefile + Docker-Compose + main.py приложены в проекте 

Каталог и dockerignore
```
ls -la
total 104
drwxrwxr-x  6 sypchik sypchik  4096 Jul  9 16:11 .
drwxr-x--- 11 sypchik sypchik  4096 Jul  9 15:03 ..
-rw-rw-r--  1 sypchik sypchik   600 Jul  9 16:09 docker-compose.yml
-rw-rw-r--  1 sypchik sypchik   180 Jul  9 16:11 Dockerfile.python
-rw-rw-r--  1 sypchik sypchik    66 Jul  9 16:07 .dockerignore
-rw-rw-r--  1 sypchik sypchik   102 Jul  9 14:06 .env
drwxrwxr-x  8 sypchik sypchik  4096 Jul  9 14:06 .git
drwxrwxr-x  3 sypchik sypchik  4096 Jul  9 14:06 haproxy
-rw-rw-r--  1 sypchik sypchik    32 Jul  9 15:57 ip.cnf
-rw-rw-r--  1 sypchik sypchik  1036 Jul  9 14:06 LICENSE
-rw-rw-r--  1 sypchik sypchik  1316 Jul  9 14:06 main.py
drwxr-xr-x  2 root    root     4096 Jul  9 15:58 my.cnf
drwxrwxr-x  3 sypchik sypchik  4096 Jul  9 14:06 nginx
-rw-rw-r--  1 sypchik sypchik   567 Jul  9 14:06 proxy.yaml
-rw-rw-r--  1 sypchik sypchik   928 Jul  9 14:06 README.md
-rw-rw-r--  1 sypchik sypchik    29 Jul  9 14:06 requirements.txt
-rw-rw-r--  1 sypchik sypchik 39767 Jul  9 14:06 schema.pdf

cat .dockerignore
__pycache__
*.pyc
*.pyo
*.pyd
venv
.env
.DS_Store
.git
.gitignore

```
Вывод запущенного композа
```
sypchik@netology:~/shvirtd-example-python$ docker compose up
[+] Running 3/2
 ✔ Network shvirtd-example-python_default  Created                                                                               0.1s
 ✔ Container mysql                         Created                                                                               0.1s
 ✔ Container app                           Created                                                                               0.0s
Attaching to app, mysql
mysql  | 2024-07-09 16:26:07+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.1-1.el9 started.
mysql  | 2024-07-09 16:26:07+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
mysql  | 2024-07-09 16:26:07+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.1-1.el9 started.
mysql  | 2024-07-09 16:26:07+00:00 [Note] [Entrypoint]: Initializing database files
mysql  | 2024-07-09T16:26:07.871988Z 0 [System] [MY-015017] [Server] MySQL Server Initialization - start.
mysql  | 2024-07-09T16:26:07.873406Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.4.1) initializing of server in progress as process 80
mysql  | 2024-07-09T16:26:07.881829Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
app    | Traceback (most recent call last):
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 334, in _open_connection
app    |     self._cmysql.connect(**cnx_kwargs)
app    | _mysql_connector.MySQLInterfaceError: Can't connect to MySQL server on 'db:3306' (111)
app    |
app    | The above exception was the direct cause of the following exception:
app    |
app    | Traceback (most recent call last):
app    |   File "/app/main.py", line 14, in <module>
app    |     db = mysql.connector.connect(
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/pooling.py", line 322, in connect
app    |     return CMySQLConnection(*args, **kwargs)
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 151, in __init__
app    |     self.connect(**kwargs)
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/abstracts.py", line 1399, in connect
app    |     self._open_connection()
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 339, in _open_connection
app    |     raise get_mysql_exception(
app    | mysql.connector.errors.DatabaseError: 2003 (HY000): Can't connect to MySQL server on 'db:3306' (111)
app exited with code 0
mysql  | 2024-07-09T16:26:22.660379Z 0 [System] [MY-015018] [Server] MySQL Server Initialization - end.
mysql  | 2024-07-09 16:26:22+00:00 [Note] [Entrypoint]: Database files initialized
mysql  | 2024-07-09 16:26:22+00:00 [Note] [Entrypoint]: Starting temporary server
mysql  | 2024-07-09T16:26:22.716326Z 0 [System] [MY-015015] [Server] MySQL Server - start.
mysql  | 2024-07-09T16:26:22.970181Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.4.1) starting as process 119
mysql  | 2024-07-09T16:26:22.998348Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
mysql  | 2024-07-09T16:26:25.166756Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
mysql  | 2024-07-09T16:26:25.964496Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
mysql  | 2024-07-09T16:26:25.964536Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
mysql  | 2024-07-09T16:26:25.970405Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
mysql  | 2024-07-09T16:26:26.694273Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: /var/run/mysqld/mysqlx.sock
mysql  | 2024-07-09T16:26:26.694554Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.4.1'  socket: '/var/run/mysqld/mysqld.sock'  port: 0  MySQL Community Server - GPL.
mysql  | 2024-07-09 16:26:26+00:00 [Note] [Entrypoint]: Temporary server started.
mysql  | '/var/lib/mysql/mysql.sock' -> '/var/run/mysqld/mysqld.sock'
mysql  | Warning: Unable to load '/usr/share/zoneinfo/iso3166.tab' as time zone. Skipping it.
mysql  | Warning: Unable to load '/usr/share/zoneinfo/leap-seconds.list' as time zone. Skipping it.
mysql  | Warning: Unable to load '/usr/share/zoneinfo/leapseconds' as time zone. Skipping it.
app    | Traceback (most recent call last):
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 334, in _open_connection
app    |     self._cmysql.connect(**cnx_kwargs)
app    | _mysql_connector.MySQLInterfaceError: Can't connect to MySQL server on 'db:3306' (111)
app    |
app    | The above exception was the direct cause of the following exception:
app    |
app    | Traceback (most recent call last):
app    |   File "/app/main.py", line 14, in <module>
app    |     db = mysql.connector.connect(
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/pooling.py", line 322, in connect
app    |     return CMySQLConnection(*args, **kwargs)
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 151, in __init__
app    |     self.connect(**kwargs)
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/abstracts.py", line 1399, in connect
app    |     self._open_connection()
app    |   File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 339, in _open_connection
app    |     raise get_mysql_exception(
app    | mysql.connector.errors.DatabaseError: 2003 (HY000): Can't connect to MySQL server on 'db:3306' (111)
mysql  | Warning: Unable to load '/usr/share/zoneinfo/tzdata.zi' as time zone. Skipping it.
mysql  | Warning: Unable to load '/usr/share/zoneinfo/zone.tab' as time zone. Skipping it.
mysql  | Warning: Unable to load '/usr/share/zoneinfo/zone1970.tab' as time zone. Skipping it.
mysql  | 2024-07-09 16:26:29+00:00 [Note] [Entrypoint]: Creating database virtd
mysql  | 2024-07-09 16:26:29+00:00 [Note] [Entrypoint]: Creating user app
mysql  | 2024-07-09 16:26:29+00:00 [Note] [Entrypoint]: Giving user app access to schema virtd
mysql  |
mysql  | 2024-07-09 16:26:29+00:00 [Note] [Entrypoint]: Stopping temporary server
mysql  | 2024-07-09T16:26:29.703039Z 13 [System] [MY-013172] [Server] Received SHUTDOWN from user root. Shutting down mysqld (Version: 8.4.1).
mysql  | 2024-07-09T16:26:31.254993Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.4.1)  MySQL Community Server - GPL.
mysql  | 2024-07-09T16:26:31.255017Z 0 [System] [MY-015016] [Server] MySQL Server - end.
mysql  | 2024-07-09 16:26:31+00:00 [Note] [Entrypoint]: Temporary server stopped
mysql  |
mysql  | 2024-07-09 16:26:31+00:00 [Note] [Entrypoint]: MySQL init process done. Ready for start up.
mysql  |
mysql  | 2024-07-09T16:26:31.722088Z 0 [System] [MY-015015] [Server] MySQL Server - start.
mysql  | 2024-07-09T16:26:31.970661Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.4.1) starting as process 1
mysql  | 2024-07-09T16:26:31.976617Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
mysql  | 2024-07-09T16:26:34.496541Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
mysql  | 2024-07-09T16:26:35.400898Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
mysql  | 2024-07-09T16:26:35.400939Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
mysql  | 2024-07-09T16:26:35.407880Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
mysql  | 2024-07-09T16:26:35.910160Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
mysql  | 2024-07-09T16:26:35.910389Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.4.1'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
app    |  * Serving Flask app 'main'
app    |  * Debug mode: on
app    | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
app    |  * Running on all addresses (0.0.0.0)
app    |  * Running on http://127.0.0.1:5000
app    |  * Running on http://172.18.0.3:5000
app    | Press CTRL+C to quit
app    |  * Restarting with stat
app    |  * Debugger is active!
app    |  * Debugger PIN: 120-213-719
^CGracefully stopping... (press Ctrl+C again to force)
```
Запуск проекта локально
![image](https://github.com/Borschik27/netologyHW2/assets/121562626/08dff386-edc1-4a2e-9e4d-b580bb0f0e31)
```
(.venv) sypchik@netology:~$ sudo apt intall python3 python3-venv > /dev/null 2>&1

(.venv) sypchik@netology:~$ python3 -m venv /home/sypchik/.venv
(.venv) sypchik@netology:~$ pip install --upgrade pip > /dev/null 2>&1
(.venv) sypchik@netology:~$ pip install -r shvirtd-example-python/requirements.txt > /dev/null 2>&1
(.venv) sypchik@netology:~$ python3 shvirtd-example-python/main.py
 * Serving Flask app 'main'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://10.128.0.6:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 115-082-689
```
В main.py добавлена библиотека и строка кода для использования .env
```
from dotenv import load_dotenv

load_dotenv(dotenv_path=os.path.join(os.path.dirname(__file__), '/home/sypchik/.env'))
```
Для создания своей таблицы добавлена переменная и изменен код где reqests заменен на переменную
```
table_name = os.environ.get('TABLE_NAME', 'requests')
# SQL-запрос для создания таблицы в БД
create_table_query = f"""
CREATE TABLE IF NOT EXISTS {db_database}.{table_name} (
id INT AUTO_INCREMENT PRIMARY KEY,
request_date DATETIME,
request_ip VARCHAR(255)
)
"""
cursor.execute(create_table_query)

sypchik@netology:~$ cat /home/sypchik/.env
DB_HOST=10.128.0.6
DB_USER=app
DB_PASSWORD=QwErTy1234
DB_NAME=virtd
TABLE_NAME=test
```

Задание 2 

```
sypchik@netology:~$ docker images
REPOSITORY                                TAG                        IMAGE ID       CREATED         SIZE
cr.yandex/crpgm4k9ci5g631sutij/pythonhw   1.0.0                      f7586efbade4   4 minutes ago   227MB
shvirtd-example-python-app                latest                     ffb8ea077e61   19 hours ago    227MB
netologyhw                                1.0.0                      e7c3e939b06c   21 hours ago    227MB
tastysypchik/netology                     AU-custom-nginx-t2_1.0.0   2c1a49677aad   21 hours ago    188MB
mysql                                     lts                        da8f2a99cf39   8 days ago      583MB
ubuntu                                    22.04                      8a3cdc4d1ad3   12 days ago     77.9MB
centos                                    centos7                    eeb6ee3f44bd   2 years ago     204MB
sypchik@netology:~$ docker tag tastysypchik/netology:AU-custom-nginx-t2_1.0.0 cr.yandex/crpgm4k9ci5g631sutij/pythonh:1.0.0
nginx:1.0.0
sypchik@netology:~$ docker images
REPOSITORY                                TAG                        IMAGE ID       CREATED         SIZE
cr.yandex/crpgm4k9ci5g631sutij/pythonhw   1.0.0                      f7586efbade4   5 minutes ago   227MB
shvirtd-example-python-app                latest                     ffb8ea077e61   19 hours ago    227MB
netologyhw                                1.0.0                      e7c3e939b06c   21 hours ago    227MB
cr.yandex/crpgm4k9ci5g631sutij/nginx      1.0.0                      2c1a49677aad   21 hours ago    188MB
tastysypchik/netology                     AU-custom-nginx-t2_1.0.0   2c1a49677aad   21 hours ago    188MB
mysql                                     lts                        da8f2a99cf39   8 days ago      583MB
ubuntu                                    22.04                      8a3cdc4d1ad3   12 days ago     77.9MB
centos                                    centos7                    eeb6ee3f44bd   2 years ago     204MB
sypchik@netology:~$ docker push cr.yandex/crpgm4k9ci5g631sutij/nginx:1.0.0
The push refers to repository [cr.yandex/crpgm4k9ci5g631sutij/nginx]
d5b0564556ee: Pushed
1091814e6af8: Pushed
cd8d591df8d7: Pushed
ad2f52a870b6: Pushed
28bc3c939a8d: Pushed
b503a08457e3: Pushed
19d8180bc03a: Pushed
32148f9f6c5a: Layer already exists
1.0.0: digest: sha256:ffd0d604ca8b3ea755cb4e6aae8e61231c6e390d84666da92441a1ab620df32c size: 1985
```
![image](https://github.com/Borschik27/netologyHW2/assets/121562626/b914676d-6388-45fe-853b-4e0455566959)

Задача 3
![image](https://github.com/Borschik27/netologyHW2/assets/121562626/20ae47ee-257e-4937-a9f1-78aae5097262)

Задача 4 

![image](https://github.com/Borschik27/netologyHW2/assets/121562626/88422e30-0953-4c0b-b9e2-c6ba554683da)

Форк-репо
https://github.com/Borschik27/shvirtd-example-python

```
sypchik@netology:~/shvirtd-example-python$ cat forkHW.sh
#!/bin/sh
wd=/opt/myProj
git clone https://github.com/Borschik27/shvirtd-example-python.git $wd
chown -R $(id -u):$(id -g) $wd
docker compose -f $wd/docker-compose.yml up
```
Задача 5
Задачу реализовать быстро к сожалению не могу выдает таку ошибку
![image](https://github.com/Borschik27/netologyHW2/assets/121562626/16341c18-c2e3-40ec-8d49-db3402b41b8b)

Задача 6
```
sypchik@netology:~$ docker pull hashicorp/terraform:latest
latest: Pulling from hashicorp/terraform
Digest: sha256:4826ea916b3678ffbe091380f0571cc2b097360c6e1624168e7a543284d576a4
Status: Image is up to date for hashicorp/terraform:latest
docker.io/hashicorp/terraform:latest
sypchik@netology:~$ docker save -o terraform_latest.tar hashicorp/terraform:latest
sypchik@netology:~$ mkdir terraform_image
tar -xvf terraform_latest.tar -C terraform_image
235b4016b0907df5897c705099d22ee37ec0bf1338ac2586e24b33b611127875/
235b4016b0907df5897c705099d22ee37ec0bf1338ac2586e24b33b611127875/VERSION
235b4016b0907df5897c705099d22ee37ec0bf1338ac2586e24b33b611127875/json
235b4016b0907df5897c705099d22ee37ec0bf1338ac2586e24b33b611127875/layer.tar
2e74ef4dd3d495f885dcdeea61843955aa1a1d7cb87c53d2b02f8b6a8cbc7d90/
2e74ef4dd3d495f885dcdeea61843955aa1a1d7cb87c53d2b02f8b6a8cbc7d90/VERSION
2e74ef4dd3d495f885dcdeea61843955aa1a1d7cb87c53d2b02f8b6a8cbc7d90/json
2e74ef4dd3d495f885dcdeea61843955aa1a1d7cb87c53d2b02f8b6a8cbc7d90/layer.tar
af62ce8c3aedebc8aedfc28dc978ab63ceb66fba41726accc1576d7ebb82b1c9.json
d8e621470ed1598249637cd6a4aea90917d4b0428b8b183a5ce85c94e033327d/
d8e621470ed1598249637cd6a4aea90917d4b0428b8b183a5ce85c94e033327d/VERSION
d8e621470ed1598249637cd6a4aea90917d4b0428b8b183a5ce85c94e033327d/json
d8e621470ed1598249637cd6a4aea90917d4b0428b8b183a5ce85c94e033327d/layer.tar
fdceaee17ed0af343d6eca575abc4a309bf066ad744a1d31fc4d9904ce9109de/
fdceaee17ed0af343d6eca575abc4a309bf066ad744a1d31fc4d9904ce9109de/VERSION
fdceaee17ed0af343d6eca575abc4a309bf066ad744a1d31fc4d9904ce9109de/json
fdceaee17ed0af343d6eca575abc4a309bf066ad744a1d31fc4d9904ce9109de/layer.tar
manifest.json
repositories
sypchik@netology:~$ find terraform_image -name terraform
sypchik@netology:~$ cd terraform_image
sypchik@netology:~/terraform_image$ find * | grep terraform
sypchik@netology:~/terraform_image$ cd ..
sypchik@netology:~$ find terraform_image -type f -executable -name terraform
sypchik@netology:~$ mkdir -p extracted_layers
sypchik@netology:~$ for layer_tar in $(find . -name "layer.tar"); do \
    tar -xf $layer_tar -C extracted_layers \
done
sypchik@netology:~$ ls
command.txt  conf.d  docker-compose.yml  Dockerfile.python  html                    snap             terraform_latest.tar
compose      data    Dockerfile          extracted_layers   shvirtd-example-python  terraform_image  yandex-cloud
sypchik@netology:~$ ls extracted_layers/
bin  dev  etc  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
sypchik@netology:~$ find extracted_layers -type f -name terraform
extracted_layers/bin/terraform
```
