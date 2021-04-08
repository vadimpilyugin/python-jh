## The Littlest JupyterHub

The Littlest JupyterHub - версия JupyterHub для небольшого числа пользователей (1-100), запущенная на одной машине. Для установки необходима Ubuntu 18.04 или больше, более ранние версии не поддерживаются.

## Установка JupyterHub

1. Установить пакеты python3, python3-dev, curl и git
```bash
sudo apt install python3 python3-dev git curl
```
2. Воспользоваться скриптом bootstrap.py, который можно загрузить с сайта TLJH либо из этого репозитория. Во второй команде нужно указать имя пользователя, который будет администратором. В дальнейшем он сможет добавить других пользователей и администраторов
```bash
curl -O https://tljh.jupyter.org/bootstrap.py
sudo -E python3 bootstrap.py --admin <admin-user-name>
```
3. Если установка завершилась успешно, то на порту 80 будет запущен веб-сервер. Для аутентификации используется имя администратора и любой пароль. При первом входе пароль сохраняется.

На этом установка завершена

## Конфигурация JupyterHub

Следующие шаги в работе с JupyterHub это настройка окружения, создание пользователей и установка SSL сертификатов.

### Добавление пользователей

Вся конфигурация осуществляется через веб-интерфейс. В браузере нужно зайти на http://localhost и использовать логин и пароль администратора.

1. Нажмите на кнопку Control Panel в правом верхнем углу
<img src="/images/control-panel-button2.png" style="display: block;">
2. В панели управления нажмите на кнопку Admin
![Admin Panel](/images/admin-access-button2.png)
Это откроет панель администратора, где можно создавать и удалять пользователей, запускать и останавливать 
3. В панели администратора нажмите на кнопку Add Users
![Add Users](/images/add-users-button1.png)
4. Можно добавить сразу несколько пользователей, по одному на строку
![Multiple users](/images/add-users-dialog1.png)

### Настройка окружения

User Environment это окружение, которое доступно всем пользователям. Администраторы могут устанавливать пакеты через sudo -E. 

1. Залогиньтесь как администратор в JupyterHub и откройте окно терминала в веб-интерфейсе
![Terminal window button](/images/new-terminal-button3.png)
2. Для установки пакетов воспользуйтесь командой conda
```bash
sudo -E conda install -c <channel-name> <package-name>
```
Важно использовать флаг -E!
3. Для установки через pip воспользуйтесь командой
```bash
sudo -E pip install <package-name>
```

Если у пользователя уже запущен сервер Jupyter, то нужно его перезапустить, чтобы пакеты стали доступны.

### Установка SSL сертификатов

JupyterHub поддерживает автоматическое получение сертификатов через Let's Encrypt. Чтобы включить поддержку HTTPS, выполните следующие действия

1. Поменяйте конфигурацию через tljh-config
```bash
sudo tljh-config set https.enabled true
sudo tljh-config set https.letsencrypt.email you@example.com
sudo tljh-config add-item https.letsencrypt.domains yourdomain.com
```
2. Проверьте, что конфигурация изменилась
```bash
sudo tljh-config show
```
```bash
https:
  enabled: true
  letsencrypt:
    email: you@example.com
    domains:
    - yourdomain.com
```
3. Перезапустите прокси-сервер
```bash
sudo tljh-config reload proxy
```

После этого JupyterHub запросит сертификаты у Let's Encrypt и будет автоматически их обновлять каждые 3 месяца.