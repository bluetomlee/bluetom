title: "php转xls"
date: 2014-12-21 00:56:37
tags:
---

毕业设计做到php导出xls

选课课表阶段时候，网上资料各种坑

自己改下

贴上代码

    <?php

    // Datebase Config

    $server="localhost";
    $database="xuanke";
    $databaseuser="root";
    $databasepassword="";
    $table="tb_course";

    $e = new Excel();   //实例化
    $savename = date("YmjHis").".xls"; //导出excel文件名
    $e->generar($server,$database,$databaseuser,$databasepassword,$table,$savename);

    class Conector {
            function abrirbase($server,$database,$dbuser,$pass) {
                $link=mysql_connect($server,$dbuser,$pass);
                if (!$link)
                    die("
    faild");
                    mysql_set_charset("utf8",$link);
                    mysql_select_db($database,$link)
                or die ("
    $database:".mysql_error());
                return $link;
            }
    }

    class Excel {

        private $conector;

        function generar($server,$database,$dbuser,$pass,$table,$nombreArchivo) {
            $c=new Conector();
            $c->abrirbase($server,$database,$dbuser,$pass);

            $querytxt="SELECT * FROM ".$table.";";
            $result=mysql_query($querytxt);

            if (mysql_error()) {
                die("
    ".mysql_error());
            }

            if (mysql_num_rows($result)==0) {
                die("
    没有此表");
            }

        // Functions for export to excel.
            function xlsBOF() {
            echo pack("ssssss", 0x809, 0x8, 0x0, 0x10, 0x0, 0x0);
            return;
            }
            function xlsEOF() {
                echo pack("ss", 0x0A, 0x00);
                return;
            }
        function xlsWriteNumber($Row, $Col, $Value) {
            echo pack("sssss", 0x203, 14, $Row, $Col, 0x0);
            echo pack("d", $Value);
        return;
    }
        function xlsWriteLabel($Row, $Col, $Value ) {
            $Value = iconv("UTF-8", "gb2312", $Value);  //强制转换GBK
            $L = strlen($Value);
            echo pack("ssssss", 0x204, 8 + $L, $Row, $Col, 0x0, $L);
            echo $Value;
            return;
        }

    header("Pragma: public");
    header("Expires: 0");
    header("Cache-Control: must-revalidate, post-check=0, pre-check=0");
    header("Content-Type: application/force-download");
    header("Content-Type: application/octet-stream");
    header("Content-Type: application/download");;
    header("Content-Disposition: attachment;filename=".$nombreArchivo);
    header("Content-Transfer-Encoding: binary ");

    xlsBOF();

    $i = 0;
    while ($i < mysql_num_fields($result)) {
        $meta = mysql_fetch_field($result, $i);
        if (!$meta) {
            echo "nopes\n";
        }
        xlsWriteLabel(0,$i,$meta->name);
        $fieldnames[$i]=$meta->name;
        $fieldtype[$i]=$meta->numeric;
        $i++;
    }

    $xlsRow = 1;
    $j=0;

    while($row=mysql_fetch_array($result)){
        for ($j=0;$j<$i;$j++) {
            if ($fieldtype[$j]==0) {
                xlsWriteLabel($xlsRow,$j,$row[$fieldnames[$j]]);
            }
            else {
                xlsWriteNumber($xlsRow,$j,$row[$fieldnames[$j]]);
            }
        }

    $xlsRow++;
    }
    xlsEOF();
    }
    }
    ?>

    ?&gt;
    