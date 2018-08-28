# createSitemap

```php
function createSitemap($siteId = "s1")
{
    if (CModule::IncludeModule('search')) {
        $NS = Array();
        $sm_max_execution_time = 0;
        $sm_record_limit = 5000;
        do {
            $cSiteMap = new CSiteMap;
            $NS = $cSiteMap->Create(
                $siteId,
                array(
                    $sm_max_execution_time,
                    $sm_record_limit
                ),
                $NS
            );
        } while (is_array($NS));
    }
    return "createSitemap(\"" . $siteId . "\");";
}
```
