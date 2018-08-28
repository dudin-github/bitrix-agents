# Список агентов

[exportToYandex](./agents/exportToYandex.md)
[createSitemap](./agents/createSitemap.md)

# Список событий

[changeIBElementProperty](./events/changeIBElementProperty.md)
[createBrand](./events/createBrand.md)
[myCurrencyFormat](./events/myCurrencyFormat.md)
[sendOrderMessage](./events/sendOrderMessage.md)

# Подключить все содержимое папок

Добавьте в init.php следующий код

```php
foreach (array("/events", "/functions", "/agents") as $dir) {
    $dir = dirname(__FILE__) . $dir;
    $dirHandler = opendir($dir);
    while ($file = readdir($dirHandler)) {
        if ($file != "." && $file != "..") {
            require_once $dir . "/" . $file;
        }
    }
    closedir($dirHandler);
}
```