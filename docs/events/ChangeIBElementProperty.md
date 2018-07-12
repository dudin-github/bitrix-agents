# YandexExport

```php
AddEventHandler("iblock", "OnAfterIBlockElementUpdate", "changeIBElementProperty");
AddEventHandler("iblock", "OnAfterIBlockElementAdd", "changeIBElementProperty");

function changeIBElementProperty(&$arFields)
{
    CModule::IncludeModule('iblock');
    
    $IBLOCK_ID = 1;
    $PROPERTY_CODE = 1;

    if($arFields["IBLOCK_ID"] == $IBLOCK_ID){
        CIBlockElement::SetPropertyValuesEx(
            $arFields["ID"], 
            false, 
            array(
                $PROPERTY_CODE => "Custom " . $arFields["PROPERTY_VALUES"][$PROPERTY_CODE]["VALUE"]
            )
        );
    }       
} 
```
