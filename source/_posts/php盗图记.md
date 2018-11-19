title: "#php盗图记"
date: 2014-06-06 23:11:19
tags:
---

#php盗图记

摔，搞了一个多小时也没搞出来，单个$url传值，可以下载下载

for循环,foreach都未果，图片都出现object not found。

考试完再吧

    &lt;!--?php &lt;br ?--&gt; function get_file($url,$folder,$pic_name){
    set_time_limit(24*60*60); //限制最大的执行时间
    $destination_folder=$folder?$folder.&amp;#039;/&amp;#039;:&amp;#039;&amp;#039;; //文件下载保存目录
    $newfname=$destination_folder.$pic_name;//文件PATH
    $file=fopen($url,&amp;#039;rb&amp;#039;);

    if($file){
    $newf=fopen($newfname,&amp;#039;wb&amp;#039;);
    if($newf){
    while(!feof($file)){
    fwrite($newf,fread($file,1024*8),1024*8);
    }
    }
    if($file){
    fclose($file);
    }
    if($newf){
    fclose($newf);
    }
    }
    }
    for($i=11901101,$j=0;$i&lt;=11901141;$i++,$j++){ $now=substr($i,-2); if($now==41) {$i=$i+60;} $url[$j]="http://jxgl.hdu.edu.cn/readimagexs.aspx?xh=".$i."&amp;lb=xsdzzcxx"; $file[]=$i.".jpg"; } foreach ($url as $a) { get_file($a,"all","1.jpg"); } ?&gt;
    