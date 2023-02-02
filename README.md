# Домашнее задание к занятию "`9.4. Prometheus`" - `Барановский Станислав`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

## Задание 1

Установите Prometheus

*Приведите скриншот systemctl status prometheus, где будет написано: prometheus.service — Prometheus Service Netology Lesson 9.4 — [Ваши ФИО].*
```
```
![Скриншот systemctl status prometheus](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-1.png "Скриншот systemctl status prometheus")

---

## Задание 2

Установите Node Exporter.

*Приведите скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО].*
```
```
![Скриншот systemctl status node-exporter](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-2.png "Скриншот systemctl status node-exporter")

---

## Задание 3

Подключите Node Exporter к серверу Prometheus.

*Приложите скриншот конфига из интерфейса Prometheus вкладки Status > Configuration. Приложите скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта.*
```
```
![Скриншот конфига из интерфейса Prometheus вкладки Status > Configuration](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-3-1.png "Скриншот конфига из интерфейса Prometheus вкладки Status > Configuration")
![Скриншот конфига из интерфейса Prometheus вкладки Status > Configuration](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-3-2.png "Скриншот конфига из интерфейса Prometheus вкладки Status > Configuration")

---

## Задание 4*

Установите Grafana.

*Приложите скриншот левого нижнего угла интерфейса, чтобы при наведении на иконку пользователя были видны ваши ФИО.*
```
```
![Скриншот интерфейса](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-4.png "Скриншот интерфейса")

---

## Задание 5*

Интегрируйте Grafana и Prometheus.

*Приложите скриншот дашборда (ID:11074) с поступающими туда данными из Node Exporter.*
```
```
![Скриншот дашборда](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-5.png "Скриншот дашборда")

---
