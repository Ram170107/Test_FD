## Задание: 
Задание:
Полноценный веб сервер, NGINX (Apache) + MariaDB (MySQL) + PHP , и опубликовать любой сайт, можно в соседней машинке развернуть контейнер и просто открыть страницу через прокси. Результат предоставить в любом удобной форме, со скриншотами о проделанной работы

### Выполнение:
 На облачном сервере ( в моём случае Selectel) установил OS Ubuntu 24.04 LTS 64-bit.
 Далее при помощи команды 
 
 > sudo apt update

![]()

 обновил список пакетов.
 
 Теперь можно установить на нашу систему NGINX командой 
 
 > sudo apt install nginx -y

 **-y** чтобы на вопрос "да" или "нет" ответ был "да"

![](https://github.com/Ram170107/Test_FD/blob/d27ba0aadd21561d9772731a18a373cbd2d9cf7d/screen%20/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20NGINX.png)

 Добавим NGINX в автозагрузку

 > sudo systemctl enable --now nginx


 Убедимся что NGINX запущен:

 > sudo systemctl status nginx

![]()

#### Некоторые команды для работы с NGINX:

    sudo systemctl start nginx — запуск веб-сервера;
    sudo systemctl restart nginx — перезапуск;
    sudo systemctl reload nginx — перезагрузка;
    sudo systemctl stop nginx — отключение;
    sudo systemctl status nginx — проверка состояния сервера;
    sudo nginx -t — тестирование конфигурации.

![]()
