# Найстройка защиты от индексации на web сервере apache2
#### Опасность индексации заключается в том, что конфиденциальные, служебные или технические страницы сайта, не предназначенные для публичного доступа.
Например админ-панели остаются видны пользователям, что оставляет злоумышленникам возможность брутфорса паролей.

Самое верное и простое решение ограничить доступ в ту или иную дирректорию сервера

1. Открываем конфигурационный файл apache2
```
/etc/apache2/apache2.conf
```

2. Далее находим раздел c directory specifications и добавляем следующие строки:
```
<Directory /var/www/название_вашего_проекта> ## куда хотим убрать доступ 
        AllowOverride All
        Options -Indexes
        ServerSignatures off 
</Directory>
```

Находим строки:
```
<Directory /var/www/>
        AllowOverride None
        Require all granted 
</Directory>
```

Меняем их на:
```
<Directory /var/www/>
        Options -Indexes
        Require all granted 
</Directory>
```

AllowOverride All - включаем проверку каждого запроса через файл .htaccess
Options -Indexes - отключаем индексацию
ServerSignatures off - Скрываем информацию о подключении 

Открываем файл настройки доступа от root:
```
/var/www/название_проекта/.htaccess
```

Вписываем строку:
```
Option -Indexes
```
Выходим, сохраняя изменения 

Перезапускаем apache2:
```
sudo systemctl restart apache2
```

### Настройка завершена 
