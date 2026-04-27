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

 **-y** чтобы на вопрос "да" или "нет" ответ был "да" (yes)

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

##### Также теперь мы можем проверить работу нашего сервера пройдя по ip (79.141.74.140) адресу сервера:

![](https://github.com/Ram170107/Test_FD/blob/1f791a6bbef4c7d41262d0a1237514b37a46b4a2/screen%20/NGINX_%D0%BF%D1%80%D0%B8%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F%20%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0.png)

Здесь мы видим начальную страницу NGINX по умолчанию

#### Далее устанавливаем MariadB командой:

> sudo apt install mariadb-server -y

![](https://github.com/Ram170107/Test_FD/blob/70b8dc2650c77f95a2d852a804be5306fe4ae28c/screen%20/%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20mariadb.png)

После чего запустим mariadb:

> sudo systemctl enable mariadb.service


![](https://github.com/Ram170107/Test_FD/blob/70b8dc2650c77f95a2d852a804be5306fe4ae28c/screen%20/%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B2%20%D0%B0%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D1%83%20mariadb.png)

Проверим статус работы mariadb:

> sudo systemctl status mariadb.service

![](https://github.com/Ram170107/Test_FD/blob/0251185634b04d4189c3d11f394bf4b3ee14ae47/screen/%D0%A1%D1%82%D0%B0%D1%82%D1%83%D1%81%20mariadb.png)

#### Настроим политики безопасности Mariadb:
Запустим скрипт повышения безопасности:

> sudo mariadb-secure-installation

![](https://github.com/Ram170107/Test_FD/blob/1f791a6bbef4c7d41262d0a1237514b37a46b4a2/screen%20/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0%20%D0%BF%D0%BE%D0%BB%D0%B8%D1%82%D0%B8%D0%BA%20MariaDB.png)

Вопросы которые спрашивает скрипт:

- Спрашивает пароль от root системы
- Вход в базу без пароля для локальной разработки
- Спрашивает о замене пароля root к базе
- Удаляем всех анонимных пользователей
- Разрешаем ли мы удаленный доступ к базе?
- Удалить тестовую базу?
- Обновить привелегии доступа к бд?


Также после всех шагов чтобы изменения политик вступили в силу перезапустим mariadb и проверим статус командам:

> sudo systemctl restart mariadb

> sudo systemctl status mariadb

![](https://github.com/Ram170107/Test_FD/blob/968cfae0d79a4c037924dd49653f563c11ddad82/screen%20/mariadb%20%D0%BF%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0%20%D0%B8%20%D1%81%D1%82%D0%B0%D1%82%D1%83%D1%81.png)

Далее можем зайти в mariadb:

> mariadb -u root -p

И посмотрим какие базы есть по умолчянию:

> SHOW DATABASE;

![](https://github.com/Ram170107/Test_FD/blob/1f791a6bbef4c7d41262d0a1237514b37a46b4a2/screen%20/%D0%92%D1%85%D0%BE%D0%B4%20%D0%B2%20%D0%91%D0%94%20%D0%B8%20%D1%81%D1%83%D1%89%20%D0%91%D0%94.png)

## Установка PHP
Установим PHP и популярные расширения:

> sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-zip php-bcmath -y

![](https://github.com/Ram170107/Test_FD/blob/ae6743d2163a16e8a6e7aab8f1604122108c1a07/screen/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0PHP%20%D0%B8%20%D1%80%D0%B0%D1%81%D1%88%D0%B8%D1%80%D0%B5%D0%BD%D0%B8%D0%B9.png)

#### Создадим БД:


```sudo mysql -u root -p -e "CREATE DATABASE my_site_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
sudo mysql -u root -p -e "CREATE USER my_site_user@localhost IDENTIFIED BY 'StrongPassword123!';"
sudo mysql -u root -p -e "GRANT ALL PRIVILEGES ON my_site_db.* TO 'my_site_user'@'localhost';"
sudo mysql -u root -p -e "FLUSH PRIVILEGES;"
sudo mysql -u root -p -e "SHOW DATABASES;"

```
### Создание PHP сайта:

Cоздать файл

> sudo mkdir -p /var/www/my_site

Переходим в него редактором

> sudo nano /var/www/my_site/index.php

В файл записываем код сайта:

```<?php
$host = 'localhost';
$dbname = 'my_site_db';
$user = 'my_site_user';
$pass = 'StrongPassword123!';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $user, $pass);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    // Создаем тестовую таблицу
    $pdo->exec("CREATE TABLE IF NOT EXISTS test_table (
        id INT AUTO_INCREMENT PRIMARY KEY,
        message VARCHAR(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    )");
    
    // Добавляем тестовую запись
    $stmt = $pdo->prepare("INSERT INTO test_table (message) VALUES (?)");
    $stmt->execute(['Сайт работает и подключен к MariaDB! ' . date('Y-m-d H:i:s')]);
    
    // Получаем последние 5 записей
    $stmt = $pdo->query("SELECT * FROM test_table ORDER BY id DESC LIMIT 5");
    $records = $stmt->fetchAll();
    
    echo "<h1>✅ Веб-сервер NGINX + PHP + MariaDB работает!</h1>";
    echo "<h2>Записи из базы данных:</h2>";
    echo "<ul>";
    foreach ($records as $record) {
        echo "<li>[{$record['created_at']}] {$record['message']}</li>";
    }
    echo "</ul>";
    echo "<p>PHP Version: " . phpversion() . "</p>";
    
} catch(PDOException $e) {
    echo "<h1>❌ Ошибка подключения к БД</h1>";
    echo "<p>" . $e->getMessage() . "</p>";
}
?>

```


![](https://github.com/Ram170107/Test_FD/blob/a841b46f254750be03ae37c5109459114143045d/screen/%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0%20%D1%81%D0%B0%D0%B9%D1%82%D0%B0.png)

### Настроика виртуального хоста NGINX:

Переходим в файл

> sudo nano /etc/nginx/sites-available/my_site

И вставляем код:

```nginx

server {
    listen 80;
    server_name _;
    root /var/www/my_site;
    index index.php index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}

```

#### Активируем сайт:

```sudo ln -s /etc/nginx/sites-available/my_site /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default 2>/dev/null
sudo nginx -t
sudo systemctl reload nginx

```
### Теперь можем проверить работу сайта!

![](https://github.com/Ram170107/Test_FD/blob/a841b46f254750be03ae37c5109459114143045d/screen/%D0%9F%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0%20%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE%20%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D0%B0.png)
