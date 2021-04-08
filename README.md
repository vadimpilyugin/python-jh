## The Littlest JupyterHub

The Littlest JupyterHub - версия JupyterHub для небольшого числа пользователей (1-100), запущенная на одной машине. Для установки необходима Ubuntu 18.04 или больше, более ранние версии не поддерживаются.

## Установка JupyterHub

1. Установить пакеты python3, python3-dev, curl и git
```bash
sudo apt install python3 python3-dev git curl
```
2. Воспользоваться скриптом bootstrap.py, который можно загрузить с сайта TLJH либо из этого репозитория. Во второй команде нужно указать имя пользователя, который будет администратором. В дальнейшем он сможет добавить других пользователей и администраторов
```
curl -O https://tljh.jupyter.org/bootstrap.py
sudo -E python3 bootstrap.py --admin <admin-user-name>
```
3. Если установка завершилась успешно, то на порту 80 будет запущен веб-сервер. Для аутентификации используется имя администратора и любой пароль. При первом входе пароль сохраняется.