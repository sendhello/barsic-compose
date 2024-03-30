# Запуск

```commandline
# Перейти в папку
cd /opt/barsic-compose

# Создание сети
docker network create -d macvlan \
    --subnet=192.168.1.0/24 \
    --gateway=192.168.1.2  \
    -o parent=eth0 \
     vlan
     
# Запуск контейнеров
docker compose up
```