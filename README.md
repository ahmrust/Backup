### Домашнее задание к занятию 3 «Резервное копирование»-Рустам Ахмадеев
Цель задания
В результате выполнения этого задания вы научитесь:
Настраивать регулярные задачи на резервное копирование (полная зеркальная копия)
Настраивать инкрементное резервное копирование с помощью rsync

Чеклист готовности к домашнему заданию
Установлена операционная система Ubuntu на виртуальную машину и имеется доступ к терминалу
Сделан клон этой виртуальной машины с другим IP адресом

1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или 
2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и вашу фамилию и имя
   - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
   - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/>
   - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern->
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
Желаем успехов в выполнении домашнего задания!

---

### Задание 1
Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию /tmp/backup
Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
На проверку направить скриншот с командой и результатом ее выполнения

Решение 1

1. Командой sudo rsync -avP --checksum --exclude=".*" ~/ /tmp/backup создадим зеркальную копию домашней директории с подсчитыванием хэш-суммы для всех файлов.
2. Убедимся, что в домашнем каталоге действительно были скрытые файлы(начинающиеся с точки).


![alt text](https://github.com/ahmrust/Backup/blob/main/img/1.png)

---

### Задание 2
Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
Резервная копия должна быть полностью зеркальной.
Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции.
Резервная копия размещается локально, в директории /tmp/backup.
На проверку направить файл crontab и скриншот с результатом работы утилиты.

Решение 2

1. `crontab`
# DO NOT EDIT THIS FILE - edit the master and reinstall.
# (/tmp/crontab.deZQN5/crontab installed on Wed Jun 14 20:30:09 2023)
# (Cron version -- $Id: crontab.c,v 2.13 1994/01/17 03:20:37 vixie Exp $)
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command
0 0 * * * /home/vboxuser/backup.sh
`````
```


2. `backup.sh`

#!/bin/bash

# Исходная директория
SOURCE_DIR="/home/vboxuser"
# Целевая директория
TARGET_DIR="/tmp/backup"
# Команда rsync. Cтандартный вывод - в /dev/null, ошибки - в лог.
rsync -a --checksum --exclude=".*" "$SOURCE_DIR" "$TARGET_DIR" > /dev/null 2>> /var/log/backup.log

# Проверка кода завершения rsync и запись лога
if [ $? -eq 0 ]; then
    echo "[$(date)] Резервное копирование успешно выполнено" >> /var/log/backup.log
else
    echo "[$(date)] Ошибка при выполнении резервного копирования" >> /var/log/backup.log
fi

```
``````
![alt text](https://github.com/ahmrust/Backup/blob/main/crontab)
![alt text](https://github.com/ahmrust/Backup/blob/main/img/2.png)

---

### Задания со звёздочкой*
Эти задания дополнительные. Их можно не выполнять. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.

### Задание 3*
Настройте ограничение на используемую пропускную способность rsync до 1 Мбит/c
Проверьте настройку, синхронизируя большой файл между двумя серверами
На проверку направьте команду и результат ее выполнения в виде скриншота
### Задание 4*
Напишите скрипт, который будет производить инкрементное резервное копирование домашней директории пользователя с помощью rsync на другой сервер.
Скрипт должен удалять старые резервные копии (сохранять только последние 5 штук).
Напишите скрипт управления резервными копиями, в нем можно выбрать резервную копию и данные восстановятся к состоянию на момент создания данной резервной копии.
На проверку направьте скрипт и скриншоты, демонстрирующие его работу в различных сценариях.

Правила приема работы:
Необходимо следовать инструкции по выполнению домашнего задания, используя для оформления репозиторий Github.
В ответе необходимо прикладывать требуемые материалы - скриншоты, конфигурационные файлы, скрипты. Необходимые материалы для получения зачета указаны в каждом задании.

Критерии оценки:
Зачет - выполнены все задания, ответы даны в развернутой форме, приложены требуемые скриншоты, конфигурационные файлы, скрипты. В выполненных заданиях нет противоречий и нарушения логики
На доработку - задание выполнено частично или не выполнено, в логике выполнения заданий есть противоречия, существенные недостатки, приложены не все требуемые материалы.
