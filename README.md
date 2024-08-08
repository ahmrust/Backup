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

 
```
```
![alt text](https://github.com/ahmrust/Backup/blob/main/img/1.png)

---

### Задание 2
Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
Резервная копия должна быть полностью зеркальной.
Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции.
Резервная копия размещается локально, в директории /tmp/backup.
На проверку направить файл crontab и скриншот с результатом работы утилиты.

Решение 2

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`


```
Поле для вставки кода...
https://github.com/ahmrust/Backup/blob/main/crontab

```

![alt text](ссылка на скриншот 1)

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
