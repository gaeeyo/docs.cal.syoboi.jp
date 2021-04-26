---
title: rss.php 
---

# rss.php

## rss.php とは

番組データをRSSで返す。
- http://cal.syoboi.jp/rss.php
- クエリ作成ツール → http://cal.syoboi.jp/util/rssbuilder

## パラメータ

- days (デフォルト:1)
    - 取得する日数(1～14)
- count (デフォルト:500)
    - 取得するプログラム数の上限
    - 指定無しの場合1000daysの範囲が広くてもこの範囲に丸められる場合があります
- start (デフォルト:現在の日時)
    - 放送時間の範囲の開始位置。終了位置はdaysによって決まる
    - lastupdateと同時利用は不可
- lastupdate (デフォルト:なし)
    - 更新日時の範囲の開始位置。終了位置はdaysによって決まる
    - startと同時利用は不可
- titlefmt (デフォルト:$(Mark)$(ShortTitle) $(SubTitleB))
    - titleに設定する文字列 (詳細は後述)
- usr (デフォルト:なし)
    - ユーザのID
- filter (デフォルト:0)
    - 表示するプログラムをフィルタする
    - 0: ユーザ設定通り、1: 強調されているタイトルのプログラムのみ、3:ユーザ設定(半透明の)
    - usrでユーザIDが指定されたときのみ有効
- alt (デフォルト:rss)
    - 出力する形式
    - rss: RSS1.0、json: JSON、ical: iCalendar
- callback
    - alt=jsonの時のみ有効
    - callback関数名

## start, lastupdate の書式

年、月、日、時、分、秒 の順で数字を指定。

|記述     |解釈|
|---|---|
|(空文字) |現在時刻|
|today  |5時区切りの時間|
|2010-04-01  |2010年4月1日5時0分0秒|
|20100401   |2010年4月1日0時0分0秒|
|2010040108  |2010年4月1日8時0分0秒|
|201004010830 |2010年4月1日8時30分0秒|
|20100401083015|2010年4月1日8時30分15秒|
どれにも当てはまらない場合、エラー400になります。

## titlefmt の書式

タイトルの書式。$(name) の書式。デフォルトは「$(Mark)$(ShortTitle) $(SubTitleB)」

|name|展開されるテキスト|サンプル|
|---|---|---|
|TID|TID|463|
|PID|PID|24496|
|Title|タイトル|こちら葛飾区亀有公園前派出所|
|ShortTitle|短いタイトル|こち亀|
|ChName|チャンネル|NHK-BS1|
|ChiEPGName|iEPG用のチャンネル名(存在しない場合はChNameと同内容)|ＮＨＫ衛星第一|
|ChID|チャンネルID|3|
|ChGID|チャンネルグループID|1|
|OffsetA|オフセット|+30|
|OffsetB|オフセット|▼30|
|Count|回数|1|
|SubTitleA|サブタイトル|笑ってユルして・・・派出所全員あっはっは|
|SubTitleB|サブタイトル|#302 「笑ってユルして・・・派出所全員あっはっは」|
|Mark|マーク|【新】|
|MarkW|警告マーク|【！】|
|Flag|フラグの数値&br;1:注/2:新/4:終/8:再|0|
|FlagW|警告フラグの数値&br;0:なし/1:先週無かったか時間が違う|0|
|StTime|開始時間|12/05 19:00|
|EdTime|終了時間|19:30|
|StTimeU|開始時間(Unix Epoch)| |
|EdTimeU|終了時間(Unix Epoch)| |
|Revision|修正回数| |
|LastUpdateU|更新時間(Unix Epoch)| |
|ConfFlag|ユーザ設定の値| |
|Cat|カテゴリ| |
