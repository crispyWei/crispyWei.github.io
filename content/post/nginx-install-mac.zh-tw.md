---
author: Bobby
title: Nginx install Mac local source
date: 2021-11-04
description: Nginx Mac 本機安裝不透過brew
---

# Nginx Mac 本機安裝
若使用brew安裝Nginx後續要進行add mudule較麻煩會發生找不到configure的情況，為防止此情況發生一開始就使用本機進行安裝配置

下載Nginx到本機
> 
>     cd /usr/local/src  #src無此目錄自行建立
>     curl -OL http://nginx.org/download/nginx-1.12.2.tar.gz ＃下載最新穩定版本
>     tar -xvzf nginx-1.12.2.tar.gz && rm nginx-1.12.2.tar.gz
>

下載PCRE Librry
PCRE函式庫提供了正規表示功能，nginx.conf內設置http_rewrite_module與location會使用到

> 
>     curl -OL https://ftp.pcre.org/pub/pcre/pcre-8.41.tar.gz
>     tar xvzf pcre-8.41.tar.gz && rm pcre-8.41.tar.gz
>

配置 Nginx
要進入到有./configure的目錄中
> 
>     cd nginx-1.12.2/
>     ./configure --with-pcre=../pcre-8.41/ 

安裝 Nginx
> 
>     [sudo] make && make install
>

Add the nginx binary to $PATH:
> 
>     export PATH="/usr/local/nginx/sbin:$PATH"
>