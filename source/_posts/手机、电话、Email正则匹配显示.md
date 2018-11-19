title: "手机、电话、Email正则匹配显示"
date: 2014-11-05 14:29:00
tags:
---

项目需求,发现之前17X段手机,老正则不在支持了

所以自己重新写了手机校验的组件,并支持显示运营商号段

首先到[wiki把内地手机端](http://zh.wikipedia.org/zh/%E4%B8%AD%E5%9B%BD%E5%86%85%E5%9C%B0%E7%A7%BB%E5%8A%A8%E7%BB%88%E7%AB%A) 理一遍

分别移动、联通、电信。三种情况分别讨论，整理如下

移动：

134-139 |  147 |  150-152  | 157-159 |  1[7|8]8  | 182-184

联通：

130-132 | 1[4|5|8]5 | 1[5|7|8]6

电信：

/^1[3|5]3|177|18[0|1|9]/.test(num)

然后用test校验，封装起来~代码如下

    function cellPhone(num) {
                var results,operator;
                if(/^1[3|4|5|7|8]\d{9}$/.test(num)){
                    if(/^13[4-9]|147|15[0-2]|15[7-9]|1[7|8]8|18[2-4|7]|1705/.test(num))
                        operator = "中国移动";
                    if(/^13[0-2]|1[4|5|8]5|1[5|7|8]6|1709/.test(num))
                        operator = "中国联通";
                    if(/^1[3|5]3|177|18[0|1|9]|1700/.test(num))
                        operator = "中国电信";
                    var results = {"result":"1","operator":operator}
                }else{
                    var results = {"result":"0","operator":""}
                }
                 return results;
    }
    `</pre>

    电话就更简单了，两种情况,有区号没区号即可

    <pre>`function phone(num){
                if(/^(0\d{2,3})?\-[0-9]\d{6,8}$/.test(num)){
                    results = 1;
                }else{
                    results = 0;
                }
                return results;             
    }
    `</pre>

    Email需求则是

    数字英文混合 + 三种特殊符号(- _ .) + 数字英文混合 @英文混合 . 英文

    Email：

    <pre>`function emailCheck(email){
                var results;
                if(/^[A-Za-zd0-9]+([-_.][A-Za-zd0-9]+)*@([A-Za-zd0-9]+[-.])+[A-Za-zd]{2,5}$/.test(email)){
                   results = 1;
                }else{
                    results = 0;
                }
                return results;
     }
    