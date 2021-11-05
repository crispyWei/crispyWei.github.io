---
author: Bobby
title: SVS ELK Log Service Windows Install
date: 2021-11-04
description: SVS ELK Log Service Windows Install
---
本文將分享如何將Elasticsearch、Logstash、Kibana、Filebeat安裝至Windows與Ubuntu平台，並自動背景執行。
![](/images/elk-workflow.png)

## SVS ELK Service on Windows

- Windows 10 Minimal
- Windows Server 2012 Minimal
- JDK 1.8.0

## Elasticsearch on Windows

1. 請至官網 https://www.elastic.co/downloads/elasticsearch 6.5.1版本
2. 檔案重新命名後放置C:\ELK\elasticsearch
3. 到C:\ELK\elasticsearch\bin資料夾下執行
```
elasticsearch-service.bat install elasticsearch-service-x64
```
4. 繼續執行 elasticsearch-service.bat manager
```
elasticsearch-service.bat manager
```
5. 點擊Start來開啟服務
6. 瀏覽器請輸入http://localhost:9200 ，會看到以下畫面:

<img src="/images/elasticsearch-image-1.png" width="300"/>
<img src="/images/elasticsearch-image-2.png" width="273"/>

7. 編輯C:\ELK\elasticsearch\config\elasticsearch.yml檔案
```
#最下方加入，避免出現跨域問題
http.cors.enabled: true
http.cors.allow-origin: "*"
```
<img src="/images/elasticsearch-image-3.png" width="300"/>

## Logstash on Windows
1. 請至官網 https://www.elastic.co/downloads/logstash 6.5.1版本
2. 檔案重新命名後放置C:\ELK\logstash
3. 在bin資料夾裡建立logstash.conf，相關配置內容請查閱附件logstash.conf，如要設定其他參數可自行定義
4. 在bin資料夾中建立run.bat內容如下:
```
logstash.bat  -f logstash.conf
```
5. 安裝logstash到windows服務：
- 從nssm官網上下載nssm壓縮檔，根據作業系統找出win32或win64中的nssm.exe
- 複製nssm.exe到C:\ELK\logstash\bin，接著叫出cmd輸入以下:
```
nssm install logstash
```
6. 安裝logstash到windows服務：
7. 出現安裝介面並選擇run.bat檔路徑，也可修改服務名稱
8. 加入依賴，因為logstash的輸出是elasticsearch，如果elasticsearch沒有啟動，logstash就無法正常工作。
9. 點擊install service按鈕，執行安裝過程。

<img src="/images/logstash-image-1.png" width="300"/>
<img src="/images/logstash-image-2.png" width="290"/>

## Kibana on Windows
1. 請至官網 https://www.elastic.co/downloads/kibana  6.5.1版本
2. 檔案重新命名後放置C:\ELK\kibana
3. 將nssm.exe複製到kibana的bin目錄下，叫出cmd輸入以下:
```
nssm install kibana
```
4. 填寫如下內容，並在依賴裡面加入對應服務名稱：點擊install service按鈕，執行安裝
<img src="/images/kibana-image-1.png" width="300"/>
<img src="/images/kibana-image-2.png" width="300"/>

## Kibana Run Browser
1. 打開cmd輸入services.msc會出現windows服務，依序啟動以下服務：
- Elasticsearch
- Logstash
- Kibana
2. 在瀏覽器中輸入: http://localhost:5601/ 即可以看到Kibana介面

