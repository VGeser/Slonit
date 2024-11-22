## Homework 8

1) Просмотр интерфейсов (интерфейс enp0s5 подключен к интернету через публичный ip)

```bash
  ip a | grep inet | grep -v 127.0.0.1
```
```bash
inet 93.183.75.9/24 brd 93.183.75.255 scope global noprefixroute enp0s5
```

2) Создать именованный пайп, вывести в файл через pipe вывод команды ss -plnt

```bash
  mkfifo pipe1
  cat pipe1 > output.txt &
  ss -plnt > pipe1
```
```bash
 cat output.txt
 State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=901,fd=5))
```

3) При помощи именованного пайпа заархивировать всё, что в него отправляем

```bash
  mkfifo pipe2
  tar -cf messages.tar -C /var/log messages < pipe2 &
  cat /var/log/messages > pipe2
```
```bash
  tar xvf messages.tar 
  head messages
  Sep 21 08:11:38 localhost root[36680]: os-prober: debug: running /usr/libexec/os-probes/mounted/80minix on mounted /dev/vda1
  Sep 21 08:11:38 localhost root[36680]: os-prober: debug: running /usr/libexec/os-probes/mounted/83haiku on mounted /dev/vda1
  Sep 21 08:11:38 localhost root[36680]: 83haiku: debug: /dev/vda1 is not a BeFS partition: exiting
```

