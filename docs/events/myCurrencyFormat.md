AddEventHandler("currency", "CurrencyFormat", "myFormat");

function myFormat($fSum, $strCurrency)
{
    return number_format ( $fSum, 2, '.', ' ' );
}