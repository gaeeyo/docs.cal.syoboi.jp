---
title: cal_chk.php 
---

# 概要

-   cal\_chk.php は cal\_chk.xml の代わりになるものです。
-   cal\_chk.xml は EUC-JP ですが、cal\_chk.php は UTF-8 で、生成も動的で、パラメータを指定することでより多くの情報を取得できます。
-   cal\_chk.xml は使わないでください。近々更新を停止する予定です。

# パラメータ

|名前|内容 |サンプル|
|---|---|---|
|usr    |UserID |usr=gae|
|cookie |0:指定なし, 1:クッキーのチャンネルフィルタを使う|cookie=1|
|start  |取得開始する日YYYY-MM-DD形式の日付 |start=2009-01-01|
|days   |取得する日数(1～30)| days=1|


取得される時間はstartで指定した5時間後からになります。

