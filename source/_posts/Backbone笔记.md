title: "Backbone笔记"
date: 2014-11-05 11:30:00
tags:
---

### 事件

#### bind

和jquery事件绑定一样机制

#### unbind

解除绑定

#### trigger

手动执行event事件

    $(function(){
        var task = Backbone.Model.extend({
            defaults: {
                id: "",
                content: "none",
                date: '1993-01-01'
            }
        });
        var daily = new task();
        daily.on("change_date",function(){
            alert("触发做了");
        });
        daily.on("change:content",function(model,value){
            if(value != undefined)
                alert("修改后的内容为" + value);
            else
                alert("触发content");
        })
        daily.trigger("change_date");
        daily.trigger("change:content");
        daily.set("content",1);
    })
    `</pre>

    ### 模型

*   extend

    <pre>`    var todo = Backbone.Model.extend({
            initialize: function(){
                console.log("初始化")
            },
            son: function(){},
            daughter:function(){}
        });
    `</pre>

    通过建造模型,先用initialize初始化函数，然后可以建立相应子类

*   get 模型后去当前属性
*   set 设置模型value,会引起change事件,可通过{silent:true}阻止
*   escape 和get一样结果,可避免xss
*   has 判断属性值为非null,依赖库underscore
*   unset 删除obj中属性

    <pre>`$(function(){
        var water = Backbone.Model.extend();
        var ocean = new water({
            id: "1",
            address: "Hangzhou"
        });
        alert(ocean.get("address"));  //Hangzhou
        ocean.unset("address");
        alert(ocean.get("address"));  //undefined
    })
    `</pre>

    当我们把unset换为clear时候发现,所有数据都获取不到，clear为模型全部清空

    <pre>`    alert(ocean.get("address"));  //Hangzhou
        ocean.clear();
        alert(ocean.get("id")); //undefined

*   clear 删除模型中所有属性数据
*