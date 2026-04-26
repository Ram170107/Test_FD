## Задание: 
Задание:
Полноценный веб сервер, NGINX (Apache) + MariaDB (MySQL) + PHP , и опубликовать любой сайт, можно в соседней машинке развернуть контейнер и просто открыть страницу через прокси. Результат предоставить в любом удобной форме, со скриншотами о проделанной работы

### Выполнение:
 На облачном сервере ( в моём случае Selectel) установил OS Ubuntu 24.04 LTS 64-bit.
 Далее при помощи команды 
 
 > sudo apt update

![](https://github.com/Ram170107/Test_FD/blob/db187c8e5b1b7ec76d566ed73286161ddca7a85a/screen%20/%D0%9E%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2.png)

 обновил список пакетов.
 
 Теперь можно установить на нашу систему NGINX командой 
 
 > sudo apt install nginx -y

 **-y** чтобы на вопрос "да" или "нет" ответ был "да"

![](https://github.com/Ram170107/Test_FD/blob/d27ba0aadd21561d9772731a18a373cbd2d9cf7d/screen%20/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20NGINX.png)

 Добавим NGINX в автозагрузку

 > sudo systemctl enable --now nginx


 Убедимся что NGINX запущен:

 > sudo systemctl status nginx

![](https://github.com/Ram170107/Test_FD/blob/db187c8e5b1b7ec76d566ed73286161ddca7a85a/screen%20/%D0%A1%D1%82%D0%B0%D1%82%D1%83%D1%81%20NGINX.png)

#### Некоторые команды для работы с NGINX:

    sudo systemctl start nginx — запуск веб-сервера;
    sudo systemctl restart nginx — перезапуск;
    sudo systemctl reload nginx — перезагрузка;
    sudo systemctl stop nginx — отключение;
    sudo systemctl status nginx — проверка состояния сервера;
    sudo nginx -t — тестирование конфигурации.

![]()

#### Далее устанавливаем MariadB
