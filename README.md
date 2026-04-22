# Домашние задания по модулю  «Отказоустойчивость» Рыльцева Виктория


В этом репозитории расположены ваши домашние задания к каждой лекции. 

Обязательны к выполнению задачи без звездочек. Их нужно выполнить, чтобы получить зачёт.

Задачи со звёздочкой (*) — дополнительные задачи или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Любые вопросы по решению задач задавайте в чате учебной группы. Ссылку вы найдёте в письме на вашей электронной почте.


1. [Disaster recovery и Keepalived](1.md)

2. [Кластеризация и балансировка нагрузки](2.md)

# Домашнее задание к занятию 2 «Кластеризация и балансировка нагрузки»
## Задание 1

**Конфигурационный файл :**

```haproxy
global
    log /dev/log local0
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin
    user haproxy
    group haproxy
    daemon

defaults
    log global
    timeout connect 5s
    timeout client 30s
    timeout server 30s

frontend front
    bind *:8088
    mode tcp
    default_backend web_servers

backend web_servers
    mode tcp
    balance roundrobin
    server s1 127.0.0.1:8888 check
    server s2 127.0.0.1:9999 check
```

### Скриншоты
![скриншот 1](https://github.com/ryltsevavikyla-coder/-/blob/main/Screenshot%202026-04-22%20144745.png)
![2](https://github.com/ryltsevavikyla-coder/-/blob/main/Screenshot%202026-04-22%20144909.png)
![3](https://github.com/ryltsevavikyla-coder/-/blob/main/Screenshot%202026-04-22%20144916.png)


# Задание 2

**Конфигурационный файл :**

```haproxy
global
    log /dev/log local0
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin
    user haproxy
    group haproxy
    daemon

defaults
    log global
    timeout connect 5s
    timeout client 30s
    timeout server 30s

frontend front
    bind *:8088
    mode http
    option httplog

    # ACL для домена example.local
    acl is_example hdr(host) -i example.local
    use_backend weighted_servers if is_example
    default_backend deny_backend

backend weighted_servers
    mode http
    balance roundrobin
    server s1 127.0.0.1:8888 check weight 2
    server s2 127.0.0.1:9999 check weight 3
    server s3 127.0.0.1:7777 check weight 4

backend deny_backend
    mode http
    http-request deny deny_status 403

```
## Скриншоты
### без домена 
![скриншот 1](https://github.com/ryltsevavikyla-coder/-/blob/main/Screenshot%202026-04-22%20174540.png)

### С доменом 
![скриншот 1](https://github.com/ryltsevavikyla-coder/-/blob/main/Screenshot%202026-04-22%20175314.png)

4. [Резервное копирование](3.md)

5. [Отказоустойчивость в облаке](4.md)

