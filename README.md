# Запуск

```commandline
# Перейти в папку
cd /opt/barsic-compose

# Создание сети
docker network create -d ipvlan \
    --subnet=192.168.1.0/24 \
    --gateway=192.168.1.2 \
    -o ipvlan_mode=l2 \
    -o parent=eth0 \
    vlan
     
# Запуск контейнеров
docker compose up
```

### Создание бекапа postgres
```commandline
# Создание бекапа postgres
ssh root@192.168.1.231
docker exec -it postgres bash
pg_dump -U barsic -W barsic > /tmp/barsic.dump
docker cp postgres:/tmp/barsic.dump /tmp/barsic.dump
exit
scp 192.168.1.231:/tmp/barsic.dump C:\\temp\barsic.dump 

# Восстановление из бекапа postgres
scp C:\\temp\barsic.dump 192.168.1.231:/tmp/barsic.dump
ssh root@192.168.1.231
docker cp /tmp/barsic.dump postgres:/tmp/barsic.dump
docker exec -it postgres bash
psql -U barsic -W barsic < /tmp/barsic.dump
```