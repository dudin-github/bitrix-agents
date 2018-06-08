AddEventHandler('main', 'OnBeforeEventAdd', 'sendOrderMessage');
	
	function sendOrderMessage($arEvent, &$lid, &$arFields)
	{
		
		if ($arEvent == "SALE_NEW_ORDER" && isset($arFields["ORDER_ID"]))
		{
			/* get currency property */
			$db_vals = CSaleOrderPropsValue::GetList(
				array("SORT" => "ASC"),
				array(
					"ORDER_ID" => $arFields["ORDER_ID"],
					"ORDER_PROPS_ID" => 10
				)
			);
			if ($arVals = $db_vals->Fetch()){
				$currency = $arVals["VALUE"];
			}
			
			/* get email property */
			$db_vals = CSaleOrderPropsValue::GetList(
				array("SORT" => "ASC"),
				array(
					"ORDER_ID" => $arFields["ORDER_ID"],
					"ORDER_PROPS_ID" => 3
				)
			);
			if ($arVals = $db_vals->Fetch()){
				$email = $arVals["VALUE"];
			}
			
			/* get currency sign */
			switch($currency){
				case("USD"):
					$currency_sign = "$";
					break;
				case("EUR"):
					$currency_sign = "€";
					break;	
				default:
					$currency_sign = "руб.";
					break;
			}
	
			/* if $arFields["ORDER_LIST"] not exist, event will canseled */
			$arFields["PRICE"] .= " " . $currency_sign;
			if(empty($arFields["ORDER_LIST"])){
				return false;
			} else {
				$arFields["ORDER_LIST"] = str_replace("\n", " " .$currency_sign . "\n", $arFields["ORDER_LIST"]);
			}
			
			if(!empty($email)){
				$arFields["EMAIL"] = $email;
			}
			
			// AddMessage2Log(json_encode($arFields), "", 1);
		}
		
	}