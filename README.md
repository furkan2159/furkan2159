Merhabalar Sizlere sitenizin her hangi bir yerinde oyun içi konusmaları site üzerinden gösterebilirsiniz  bunun anlık sorgu db oldukca yoracağından cache sistemiyle hazırladım
 5dk arayla kayıt aldına alacak kullanacak olan arkadaşlar ana dizine cache klasörü oluşturup cron eklemelisiniz.
son 10 konuşmayı gösterecek krallık bayrak ve ch detaylarını kendinize göre düzenliyebilirsiniz 

 <?php
$filenamesohbet = "anasayfa-sohbet.html";
$cachefilesohbet = "cache/".$filenamesohbet;
$cachetimesohbet = 5 * 5; // Cache Süresi
if (!(file_exists($cachefilesohbet)) || time() - $cachetimesohbet > filemtime($cachefilesohbet))
{
ob_start();
mysql_select_db("log");
?> 

<?php

        mysql_select_db('log'); //  DB seçimi 'player'
        mysql_query("SET NAMES 'utf8'");
mysql_query("SET CHARACTER SET utf8");
mysql_query("SET COLLATION_CONNECTION = 'utf8_turkish_ci'");
    $test = "SELECT * from shout_log";
        $testquery = mysql_query($test);
            $num2 = mysql_num_rows($testquery);

        if($_GET['max']) {
            $get = $_GET['max'];
        } else {
        $get = '0';
?>

<?php
        mysql_select_db('log'); // Select DB 'player'
        mysql_query("SET NAMES 'utf8'");
        mysql_query("SET CHARACTER SET utf8");
        mysql_query("SET COLLATION_CONNECTION = 'utf8_turkish_ci'");
// Select player etc from db //
    $rank = "SELECT * from shout_log WHERE channel NOT LIKE '[%]%' order by time desc limit $get,10";
        $query = mysql_query($rank);
    echo "<ul>"; // Table başı
    $i = 0;
  
            while($array = mysql_fetch_array($query)) {
                $i = $i + 1;
              
                echo "<tr>";
                echo "<td>CH " . $array["channel"] . "</td>";
                echo "<td>" . $array["time"] . "</td>";
                echo "<td><img src='images/empire" . $array["empire"] . ".png'></td>";
                echo "<td>" . $array["shout"] . "</td>";
                echo "</tr>";
                }
    echo "</ul>"; // table sonu
  
} 
?>
<?php
$fp = fopen($cachefilesohbet, 'w+');
fwrite($fp, ob_get_contents());
fclose($fp);
ob_end_flush();
}
else
{
readfile($cachefilesohbet);
}
?>

yapamayanlar discord adresimden iletişime geçebilirler .
