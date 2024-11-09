# Домашнее задание №1
## 1. Узнать IP-адрес интерфейса, подключенного к сети Интернет
```
[root@Test ~]# ip addr show | grep inet | grep -v 127.0.0.1
inet 78.140.241.71/24 brd 78.140.241.255 scope global noprefixroute enp0s5
```
## 2. Создать именованный пайп ( named pipe ). Вывести в файл через созданный pipe вывод команды ss -plnt
```
[root@Test ~]# mkfifo named_pipe
[root@Test ~]# ss -plnt > named_pipe &
[1] 9977
[root@Test ~]# cat named_pipe > output.txt
[1]+  Done                    ss -plnt > named_pipe
```
## 3. При помощи именованного пайпа заархивировать всё, что в него отправляем. Например, содержимое файла /var/log/messages. На выходе получить архив tar или любой другой
```               
[root@Test ~]# cat /var/log/messages > named_pipe &
[2] 11450
[root@Test ~]# tar -czvf archive.tar.gz named_pipe
named_pipe
```
## 4. Вывести дату в unixtime. На вход команды date через пайп подать свой формат выводимой даты
```
[root@Test ~]# echo "+%Y-%m-%d" | xargs -I {} date -d @$(date +%s) {}
2024-11-09
```
## 5. При помощи HEREDOC записать в файл многострочное сообщение.
```
[root@Test ~]# cat << HERE > file.txt
> First line
> Second line
> Third line
> HERE
```
