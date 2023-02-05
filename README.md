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
sudo useradd --no-create-home --shell /bin/false prometheus
wget https://github.com/prometheus/prometheus/releases/download/v2.42.0/prometheus-2.42.0.linux-386.tar.gz
tar xvfz prometheus-2.42.0.linux-386.tar.gz
cd prometheus-2.42.0.linux-386/
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo cp ./prometheus promtool /usr/local/bin/
sudo cp -R ./console_libraries /etc/prometheus
sudo cp -R ./consoles /etc/prometheus
sudo cp ./prometheus.yml /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
/usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ --web.console.templates=/etc/prometheus/consoles --web.console.libraries=/etc/prometheus/console_libraries
sudo nano /etc/systemd/system/prometheus.service #Содержимое файла ниже в блоке кода
sudo systemctl enable prometheus.service
sudo systemctl start prometheus.service
sudo systemctl status prometheus.service
```
Содержимое файла prometheus.service
```
[Unit]
Description=Prometheus Service Netology Lesson 9.4 - Baranovskii S.N.
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
--config.file /etc/prometheus/prometheus.yml \
--storage.tsdb.path /var/lib/prometheus/ \
--web.console.templates=/etc/prometheus/consoles \
--web.console.libraries=/etc/prometheus/console_libraries
ExecReload=/bin/kill -HUP $MAINPID Restart=on-failure
[Install]
WantedBy=multi-user.target
```

![Скриншот systemctl status prometheus](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-1.png "Скриншот systemctl status prometheus")

---

## Задание 2

Установите Node Exporter.

*Приведите скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО].*
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
tar xvfz node_exporter-1.5.0.linux-amd64.tar.gz
cd cd node_exporter-1.5.0.linux-amd64/
./node_exporter  #Проверяем доступность : http://127.0.0.1:9100/metrics
sudo mkdir /etc/prometheus/node-exporter
sudo cp ./* /etc/prometheus/node-exporter
chown -R prometheus:prometheus /etc/prometheus/node-exporter/
sudo nano /etc/systemd/system/node-exporter.service #Содержимое файла ниже в блоке кода
sudo systemctl enable node-exporter
sudo systemctl start node-exporter
sudo systemctl status node-exporter
```
Содержимое файла node-exporter.service
```
[Unit]
Description=Node Exporter Netology Lesson 9.4 - Baranovskii S.N.
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/etc/prometheus/node-exporter/node_exporter
[Install]
WantedBy=multi-user.target 
```

![Скриншот systemctl status node-exporter](https://github.com/StanislavBaranovskii/9-4-hw-prometheus/blob/main/img/9-4-2.png "Скриншот systemctl status node-exporter")

---

## Задание 3

Подключите Node Exporter к серверу Prometheus.

*Приложите скриншот конфига из интерфейса Prometheus вкладки Status > Configuration. Приложите скриншот из интерфейса Prometheus вкладки Status > Targets, чтобы было видно минимум два эндпоинта.*
```
sudo nano /etc/prometheus/prometheus.yml #Содержимое файла ниже в блоке кода
sudo systemctl restart prometheus
```
Содержимое файла prometheus.yml
```
global:
  scrape_interval: 15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets:

rule_files:

scrape_configs:
  - job_name: "prometheus"
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090', 'localhost:9100']
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
