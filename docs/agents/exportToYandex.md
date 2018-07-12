# exportToYandex

```php
function exportToYandex($exportId, $xmlFile)
{
    CModule::IncludeModule("catalog");
    CCatalogExport::PreGenerateExport($exportId);
    unlink($_SERVER["DOCUMENT_ROOT"] . "/bitrix/catalog_export/$xmlFile.xml");
    ob_start();
    include_once $_SERVER["DOCUMENT_ROOT"] . "/bitrix/catalog_export/$xmlFile.php";
    $current = ob_get_contents();
    ob_end_clean();
    file_put_contents($_SERVER["DOCUMENT_ROOT"] . "/bitrix/catalog_export/$xmlFile.xml", $current);
    unlink($_SERVER["DOCUMENT_ROOT"] . "/bitrix/catalog_export/$xmlFile.php");
}

// YM export from site "Site1"
function exportToYandexForSite1()
{
    $yandexProfileID = 1;
    $yandexFileName = "yandex_site1";

    exportToYandex($yandexProfileID, "yandex_site1");
    return "exportToYandexForSite1();";
}
```
