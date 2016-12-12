<?php
$q =$_GET["q"];//getting value from the form or you can use a direct query to test like $q="iphone 6";

$string = str_replace(" ","+", $q); //replacing white space with '+'
$string = str_replace("&","%26", $string); //replacing '&' with '%26'

/* 
Using curl in php to make a http get request to flipkart api.
Here we are setting the url to request,
required headers like affiliate id & tocken.
The given url is for results in JSON format.if you want the results to be returned in XML,please use appropriate url. 
Replace the 'YOUR ID' & 'YOUR TOKEN' with the id and token provided to you by flipkart.
*/
$curl = curl_init();
$surl="https://affiliate-api.flipkart.net/affiliate/search/json?query=".$string."&resultCount=10";//no of results to retreive is set to 10
curl_setopt_array($curl, array(
  CURLOPT_URL => $surl,
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "cache-control: no-cache",
    "fk-affiliate-id: YOUR ID",
    "fk-affiliate-token: YOUR TOKEN"
    
  ),
));
$response2 = curl_exec($curl);
$err = curl_error($curl);
curl_close($curl);
if ($err) 
{
  echo "cURL Error #:" . $err;
} 
else 
{
$response2 = utf8_encode($response2); //Encoding the response into utf8 format
$response2=json_decode($response2, true); //Decoding json string into php associative array.
}
$out=" ";
$i=0;
for($k=0;$k<10;$k++)
{

$out.='<tr style="border: 1px solid black;">

<td style="border: 1px solid black;">

<a target="_blank" href="'.$response2[productInfoList][$i][productBaseInfo][productAttributes][productUrl].'"> 

<img height="200" width="200" style="width: 30%; height: auto;" src="'.$response2[productInfoList][$i][productBaseInfo][productAttributes][imageUrls]["200x200"].'"/> </a>

 <br/>'.$response2[productInfoList][$i][productBaseInfo][productAttributes][title].'<br/>

 <b>Price:</b>INR '.$response2[productInfoList][$i][productBaseInfo][productAttributes][sellingPrice][amount].'</td></tr>';

$i++;
}
echo "<table ><tr ><th>flipkart</th></tr>".$out."</table>";
//var_dump($response2); // if you want to see the structure of received response,uncomment the var_dump.
?>
