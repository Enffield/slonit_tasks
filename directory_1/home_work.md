# Домашнее задание №1



# Задания

#### 1. Узнать IP-адрес интерфейса, подключенного к сети Интернет
```sh
[root@My-server ~] ip addr show | grep 'inet ' | grep -v 127.0.0.1
    inet 78.140.243.62/24 brd 78.140.243.255 scope global noprefixroute enp0s5
```

#### 2. Создать именованный пайп (named pipe). Вывести в файл через созданный pipe вывод команды `ss -plnt`
```sh
[root@My-server ~] mkfifo my_pipe 
[root@My-server ~] ss -plnt > my_pipe &
[1] 24846
[root@My-server ~] cat my_pipe > output.txt
[1]+  Done                    ss -plnt > my_pipe
```
#### 3. При помощи именованного пайпа заархивировать всё, что в него отправляем. Например, содержимое файла `/var/log/messages`. На выходе получить архив tar или любой другой
```sh
[root@My-server ~] mkfifo /tmp/archive_pipe
[root@My-server ~] tar czf /tmp/messages_archive.tar.gz -C /var/log messages < /tmp/archive_pipe
[root@My-server ~] cat /var/log/messages > /tmp/archive_pipe
[root@My-server ~] cd /tmp
[root@My-server tmp] ls
archive_pipe  systemd-private-a7e4f92a3da84880b95ad16070581ead-chronyd.service-IlYHLj
```
#### 4. Вывести дату в unixtime. На вход команды `date` через пайп подать свой формат выводимой даты
```sh
[root@My-server ~] date -d "2024-11-18 12:00:00 UTC" +%s
1731931200
```
#### 5. При помощи HEREDOC записать в файл многострочное сообщение
```sh
[root@My-server ~] cat > myfile.txt << END
> Мой многострочный файл
> Строка 1
> Строка 2
> Строка 3
> END
```
