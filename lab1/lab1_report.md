University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024/2025

Group: K34312

Author: Korkina Anna Mikhailovna

Lab: Lab1

Date of create: 19.09.2024

Date of finished: 27.09.2024

# Лабораторная работ №1 "Установка CHR и Ansible, настройка VPN"

### Описание
Данная работа предусматривает обучение развертыванию виртуальных машин (VM) и системы контроля конфигураций Ansible а также организации собственных VPN серверов.
### Цель работы
Целью данной работы является развертывание виртуальной машины на базе платформы Microsoft Azure с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox
### Ход работы
###### 1. Создание виртуальных машин
###### 1.1 Ubuntu

![image](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/Screenshot%20from%202024-09-26%2013-39-24.png)

#### Замечания:

- смонтирован VHD для ubuntu 18 (версия старая для экономии памяти)
- выбран сетевой адаптер : сетевой мост (для упрощения настройки ip-связности машин)

###### 1.2 Mikrotic RouterOS

![image](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/Screenshot%20from%202024-09-26%2013-39-36.png)

###### Замечания:

- смонтирован VDI для CHR 
- выбран сетевой адаптер : сетевой мост (для упрощения настройки ip-связности машин) c таким же интерфейсом что и в другой машине

###### 2. Установка python, ansible, wireguard

###### 3. Настройка wirequard server на ubuntu
###### 3.1 Создание приватного и публичного ключей


```sh
       
    wg genkey | sudo tee /etc/wireguard/private.key
    sudo chmod go= /etc/wireguard/private.key
    sudo cat /etc/wireguard/private.key | wg pubkey | sudo tee /etc/wireguard/public.key
```

###### 3.2 Написания конфигурационного файла

sudo nano /etc/wireguard/wg0.conf

![image](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/Screenshot%20from%202024-09-26%2014-07-34.png)
###### 3.3 Старт сервера 

```sh
  sudo systemctl enable wg-quick@wg0.service
```


###### 4. Настройка wirequard peer на CHR

###### 4.1 Добавление интерфейса wireguard

![image](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-41-47.jpg)


###### 4.2 Привязка IP к интерфейсу 
![images](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-50-16.jpg)


###### 4.3 Настройка firewall

![images](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-48-19.jpg)


###### 5. Тестирования туннеля

###### 5.1 ping пира с сервера 
![images](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-55-14.jpg)

###### 5.2 ping сервера с пира
![images](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-55-51.jpg)

###### 5.3 wg show для проверки трафик туннелируется 
![images](https://github.com/kegly/2024_2025-network_programming-k34212-korkina_a_m/blob/main/lab1/images/photo_2024-09-27_08-55-29.jpg)


