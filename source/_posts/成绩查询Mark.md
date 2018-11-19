title: "成绩查询Mark"
date: 2012-05-31 14:28:07
tags:
---

第一步：在网上下载一款chrome浏览器并安装

第二步：用上述浏览器进入我们学校教务系统

第三步：右键点击“信息查询”选择“单元审查”

&nbsp;

第四步：出现在方框所示的span上点击鼠标右键 选择 Edit as HTML 进入编辑状态

第五步：将这一行原有，上图红色方框中文字替换为

&lt;A onclick="GetMc('成绩查询);" href="xscj_gc.aspx?xh=学号&amp;xm=姓名&amp;gnmkdm=N121605" target=zhuti&gt;成绩查询&lt;/A&gt;

第六步：记得在上述文字中输入自己学号、姓名，点击空白处 ，发现教务系统出现“成绩查询”按钮

第七步：点击成绩查询，大功告成

再也不用别人帮你查分咯~~
_xs_main_改成lw_xscj</p>