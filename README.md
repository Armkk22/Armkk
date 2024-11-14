Установка утилиты wget на систему

    sudo yum install wget
![image](https://github.com/user-attachments/assets/7fea59ce-6111-4b64-a924-543d8e36de81)

Скачивание файла репозитория

![image](https://github.com/user-attachments/assets/6425f809-a033-42f6-a6d7-e043ee8b7eb2)

Установка докера

![image](https://github.com/user-attachments/assets/7ac90f6b-9738-4b1b-8f0f-609af6464fa9)

Запуск с дальнейшим разрешением автозапуска

![image](https://github.com/user-attachments/assets/57aa0fc4-2b88-44c9-9348-a9bd891e20d3)

Установка compose

Для начала нужно убедиться в наличии пакета curl

![image](https://github.com/user-attachments/assets/f72e550a-78e6-4cea-86eb-33476ca8f3f5)

Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose
    
Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose

![image](https://github.com/user-attachments/assets/d7de93ed-d620-492e-a017-d2bb5bc3d347)

Предоставление прав на выполнение файла docker-compose
    
    sudo chmod +x /usr/bin/docker-compose

Проверка установленной версии Docker Compose

    sudo docker-compose --version

![image](https://github.com/user-attachments/assets/6109d321-cc45-4db3-9ff2-0a33837a409d)

Делаем grafana

Установка git

    sudo yum install git

![image](https://github.com/user-attachments/assets/d76f6961-a598-4449-98fb-5f8054d6e5a8)

Этот код скачивает содержимое репозитория skl256/grafana_stack_for_docker
    
    sudo git clone https://github.com/skl256/grafana_stack_for_docker.git

![image](https://github.com/user-attachments/assets/772e34f9-0a20-4f1b-a847-2f0902b3e203)

Заходит в папку - cd
    
    cd grafana_stack_for_docker

cd .. - возвращает в папку выше
    
(После этого можно вставлять готовый docker-compose)
    
Cоздаем папки двумя разными способами

    sudo mkdir -p /mnt/common_volume/swarm/grafana/config
    
    sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data,loki-data,promtail-data}

Выдаем права
    
    sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}

Создаем файл

    sudo touch /mnt/common_volume/grafana/grafana-config/grafana.ini

Копирование файлов

    sudo cp config/* /mnt/common_volume/swarm/grafana/config/

Переименовывание файла

    sudo mv grafana.yaml docker-compose.yaml

![image](https://github.com/user-attachments/assets/687a8497-8bec-418a-b6da-3cc3d1d1c1c0)

![image](https://github.com/user-attachments/assets/ffefa797-7038-4d99-983e-335e1ec0c3f0)

Собрать докер (нужно запускать из папки где docker-compose.yaml)
    
    sudo docker compose up -d

Опустить докер - sudo docker compose stop

![image](https://github.com/user-attachments/assets/9f0a22e1-5d54-4136-ac84-d20d5015fdc8)

Начинаем чистку файлов

Команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя
        
        sudo vi docker-compose.yaml

Что-бы что-то изменить в тесковом редакторе нужно нажать insert на клавиатуре
        
Затем в docker-compose нужно вставить node-exporter и удалить ненужные файлы (но у нас уже вставлен готовый докер)

![image](https://github.com/user-attachments/assets/68cc22ed-245e-49d8-832b-f259bf733114)

выйти не сохраняясь из vim - esc -> :q!

выйти сохраняясь из vim - esc -> :wq!

Заходим в другую папку

        sudo cd /mnt/common_volume/swarm/grafana/config

Открываем файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя

        sudo vi prometheus.yaml

Далее нужно исправить targets: на exporter:9100

![image](https://github.com/user-attachments/assets/701cb955-5944-4956-b413-545a57f6c635)

Делаем grafana на сайте

переходим на сайт localhost:3000

        User & Password GRAFANA: admin

        Код графаны: 3000

        Код прометеуса: http://prometheus:9090
        
в меню выбираем вкладку Dashboards и создаем Dashboard

        ждем кнопку +Add visualization, а после "Configure a new data source"

        выбираем Prometheus

        Connection

        http://prometheus:9090
        
Authentication

        Basic authentication

        User: admin

        Password: admin

        Нажимаем на Save & test и должно показывать зелёную галочку

![image](https://github.com/user-attachments/assets/0ace0208-192a-4a57-ae0a-be64da759c0e)



        


        



    


    

