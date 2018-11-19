title: "解决Xampp登陆dedecms织梦后台空白"
date: 2013-05-07 13:39:46
tags:
---

\include\userlogin.class.php

里查找session_register

把@session_register($this->keepUserIDTag);    注释掉，然后改为

if (!isset($_SESSION[$this->keepUserIDTag]))

全部有6个。

如下：

if (!isset($_SESSION[$this->keepUserIDTag]))

//@session_register($this->keepUserIDTag);

$_SESSION[$this->keepUserIDTag] = $this->userID;

if (!isset($_SESSION[$this->keepUserTypeTag]))

//@session_register($this->keepUserTypeTag);

$_SESSION[$this->keepUserTypeTag] = $this->userType;

if (!isset($_SESSION[$this->keepUserChannelTag]))

//@session_register($this->keepUserChannelTag);

$_SESSION[$this->keepUserChannelTag] = $this->userChannel;

if (!isset($_SESSION[$this->keepUserNameTag]))

//@session_register($this->keepUserNameTag);

$_SESSION[$this->keepUserNameTag] = $this->userName;

if (!isset($_SESSION[$this->keepUserPurviewTag]))

//@session_register($this->keepUserPurviewTag);

$_SESSION[$this->keepUserPurviewTag] = $this->userPurview;

if (!isset($_SESSION[$this->keepAdminStyleTag]))

//@session_register($this->keepAdminStyleTag);

$_SESSION[$this->keepAdminStyleTag] = $adminstyle;

原因是因为Apache版本太高而不支持老函数