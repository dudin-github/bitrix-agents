---
layout: docs
title: Utilities for layout
description: For faster mobile-friendly and responsive development, Bootstrap includes dozens of utility classes for showing, hiding, aligning, and spacing content.
group: layout
toc: true
---

# Список агентов

[YandexExport](./agents/YandexExport.md)

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