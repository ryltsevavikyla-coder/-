# Домашние задания по модулю  «Отказоустойчивость»

В этом репозитории расположены ваши домашние задания к каждой лекции. 

Обязательны к выполнению задачи без звездочек. Их нужно выполнить, чтобы получить зачёт.

Задачи со звёздочкой (*) — дополнительные задачи или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Любые вопросы по решению задач задавайте в чате учебной группы. Ссылку вы найдёте в письме на вашей электронной почте.


1. [Disaster recovery и Keepalived](1.md)

2. [Кластеризация и балансировка нагрузки](2.md)

# Домашнее задание к занятию 2 «Кластеризация и балансировка нагрузки»
## Задание 1
### Задание 1 — Балансировка Round-robin на 4 уровне (TCP)

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
![скриншот 1]()
![2](images/название-файла.png)
![3](images/название-файла.png)

4. [Резервное копирование](3.md)

5. [Отказоустойчивость в облаке](4.md)

