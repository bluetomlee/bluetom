title: "php数据库连接操作类"
date: 2013-07-03 21:00:17
tags:
---

    db_host = $db_host;
    $this-&gt;db_user = $db_user;
    $this-&gt;db_password = $db_password;
    $this-&gt;db_database = $db_database;
    }
    //连接数据库
    function conn(){
    $conn = mysql_connect($this-&gt;db_host,$this-&gt;db_user,$this-&gt;db_password);
    if(!$conn){
    $this-&gt;msg_error("无法连接数据库");
    }else{
    $this-&gt;conn = $conn;
    }
    if(!mysql_select_db($this-&gt;db_database,$this-&gt;conn)){
    $this-&gt;msg_error("无法选择数据库");
    }
    return $this-&gt;conn;
    }
    //更新数据库,包括数据添加,更新
    function query_noResult($sql){
    if("" == $sql){$this-&gt;msg_error("传递了一个空变量");}
    $this-&gt;sql = $sql;
    //echo $this-&gt;sql;
    //echo $this-&gt;conn;
    if(!mysql_db_query($this-&gt;db_database,$this-&gt;sql,$this-&gt;conn)){
    $this-&gt;msg_error(("数据更新过程发生错误!"));
    }
    return null;
    }
    //查询数据并返回result类型
    function query_withResult($sql){
    if("" == $sql){$this-&gt;msg_error("传递了一个空变量");}
    $this-&gt;sql = $sql;
    // $conn = mysql_connect("localhost","root","");
    $result = mysql_db_query($this-&gt;db_database,$this-&gt;sql,$this-&gt;conn);
    //一个字母错误浪费了两个小时!真不如java
    //不过是写成了reslut

    if(!$result){
    $this-&gt;msg_error("数据查询过程发生错误或空记录!");
    }else{
    $this-&gt;result = $result;
    }
    //使用时,可以直接引用成员变量而无须关心返回值,除非需要返回值
    //做更多处理
    return $this-&gt;result;
    }
    //释放结果集
    function free(){
    mysql_free_result($this-&gt;result);
    }
    //关闭连接
    function close(){
    if($this-&gt;result){
    $this-&gt;free();
    }
    mysql_close($this-&gt;conn);
    }
    // 根据执行结果取得影响行数
    function db_affected_rows(){
    return mysql_affected_rows();
    }
    // 根据查询结果计算结果集条数
    function db_num_rows(){
    if($this-&gt;result==null){
    $this-&gt;msg_error("记录为空!");
    }
    return mysql_num_rows($this-&gt;result);
    }
    //取得记录集
    function db_fetch_array(){
    if($this-&gt;result==null){
    //$this-&gt;msg_error("您查询的记录为空!");
    }
    $this-&gt;row = @mysql_fetch_array($this-&gt;result);
    return $this-&gt;row;
    }
    //指向确定的一条数据记录
    //通用数据库错误处理
    function db_data_seek($result,$i){
    mysql_data_seek($result,$i);
    return $this-&gt;result;
    }
    function msg_error($message){
    $time = date("Y年m月d日 H时i分s秒");
    echo "很抱歉您操作数据库时发生了错误
    ";
    echo "发生错误时间:".$time."
    ";
    echo "错误信息:".$message."
    ";
    echo "请发送邮件到aofanliguo@126.com..谢谢!";
    // exit();
    }
    }
    ?&gt;

    具体使用:
    sql="";
    $this-&gt;db=$db;
    }
    //取得最新记录,可以更改sql语句得到完全控制
    function fetch_new_all(){
    $k=$this-&gt;random=Rand(4,10);
    $f=$this-&gt;random-4;
    $this-&gt;sql="select * from xl_news order by id desc limit ".$f.",".$k."";
    $result=$this-&gt;db-&gt;query_withResult($this-&gt;sql);
    $number=$this-&gt;db-&gt;db_num_rows();

    for($i=0;$i&lt;$number;$i++){ $row=mysql_fetch_array($result); $data[]=$row; } return $data; } //取得公告栏的数据并显示 function show_gonggao(){ $this-&gt;sql="select * from xl_gongao";
    $result=$this-&gt;db-&gt;query_withResult($this-&gt;sql);
    $row=mysql_fetch_array($result);
    echo "最新更新:";
    echo $row[&amp;#039;date&amp;#039;];
    echo "
    ";
    echo $row[&amp;#039;context&amp;#039;];
    }
    //提交咨询内容
    function add_advisory($name,$sex,$age,$text){
    $_name=$name;
    $_sex=$sex;
    $_age=$age;
    $_text=$text;
    $_date=date("Y-m-d H:i:s");
    $this-&gt;sql="insert into xl_zixun(name,sex,age,context,date) values(&amp;#039;$_name&amp;#039;,&amp;#039;$_sex&amp;#039;,&amp;#039;$_age&amp;#039;,&amp;#039;$_text&amp;#039;,&amp;#039;$_date&amp;#039;)";
    $this-&gt;db-&gt;query_noResult($this-&gt;sql);
    }
    }
    ?&gt;
    