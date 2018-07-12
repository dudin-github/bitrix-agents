# createBrand

```php
AddEventHandler("iblock", "OnBeforeIBlockElementUpdate", "createBrand");
AddEventHandler("iblock", "OnBeforeIBlockElementAdd", "createBrand");

function createBrand(&$arFields)
{
    $CATALOG_IBLOCK_ID = 100;
    $BRAND_IBLOCK_ID = 200;
    $BRAND_PROPERTY_ID = 300;

    if ($arFields["IBLOCK_ID"] == $CATALOG_IBLOCK_ID) {
        $arFieldsCopy = $arFields;
        $arBrandProperty = array_shift($arFieldsCopy["PROPERTY_VALUES"][$BRAND_PROPERTY_ID]);
        if ($arBrandProperty["VALUE"] != "") {
            /* Ищем элемент с названием $arBrandProperty["VALUE"] в инфоблоке брендов */
            $res = CIBlockElement::GetList(
                Array("SORT" => "ASC"),
                Array(
                    "IBLOCK_ID" => $BRAND_IBLOCK_ID,
                    "NAME" => $arBrandProperty["VALUE"]
                ),
                false,
                Array("nTopCount" => 1),
                Array("ID", "NAME")
            );
            /* Если бренд не найден - создаем */
            if (!$res->GetNext()) {
                $brandElement = new CIBlockElement;
                $arLoadProductArray = Array(
                    "IBLOCK_SECTION_ID" => false,
                    "IBLOCK_ID" => $BRAND_IBLOCK_ID,
                    "NAME" => $arBrandProperty["VALUE"],
                    "CODE" => Cutil::translit($arBrandProperty["VALUE"], "ru", array("replace_space" => "-", "replace_other" => "-")),
                    "ACTIVE" => "Y"
                );
                $brandID = $brandElement->Add($arLoadProductArray);
                if (!$brandID) {
                    AddMessage2Log("Can't create a brand: " . $brandElement->LAST_ERROR);
                }
            }
        }
    }
}
```