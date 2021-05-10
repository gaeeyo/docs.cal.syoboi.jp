---
title: db.php
---

## db.php について

データベースからXMLでデータを出力するスクリプト。  
しょぼいカレンダー内では、Flashでグラフを表示しているところで使われています。

- https://cal.syoboi.jp/db.php

Commandパラメータに取得したいデータを指定します。(Command=TitleLookup のように指定する)  
基本的にdb.phpは、テーブルの生データをそのまま出力することを目的としています。

## タイトルデータの取得 (TitleLookup)

データベースに格納されているタイトルデータをそのまま出力します。

-   TID
    -   TIDの値を指定。カンマ区切りで複数指定可能。すべてのTIDを指定するときは \* を指定
        -   TID=1
        -   TID=1,2,3
        -   TID=\*  (結果が巨大になるので注意。2009-04-21 現在で4.5MB)
-   LastUpdate
    -   LastUpdateの範囲を指定。
        -   LastUpdate=20090421\_000000- ('2009-04-21 00:00:00' <= LastUpdate)
        -   LastUpdate=-20090421\_000000 (LastUpdate < '2009-04-21 00:00:00')
        -   LastUpdate=20090301\_000000-20090401\_000000 ('2009-03-01 00:00:00' <= LastUpdate AND LastUpdate < '2009-04-01 00:00:00')
-   Fields
    -   出力するフィールドをカンマ区切りで指定。未指定の場合はすべて出力
        -   Fields=TID (TIDだけを出力する)
        -   Fields=Title,Cat (TitleとCatを出力する)

## 使用例

-   全タイトルの一覧を取得
    -   /db?Command=TitleLookup&TID=\*&Fields=TID,Title,Cat
-   TID=1853 のタイトル情報を取得
    -   /db?Command=TitleLookup&TID=1853
-   タイトルの検索
    -   json.php を参照

## 放送時間データの取得 (ProgLookup)

2009-04-22現在112,000件のデータがありますが、1回のリクエストで最大で5,000件しか出力しません。  
すべてのデータを取り出すにはStTime、Range、LastUpdateを使って対象を絞り込みリクエストを複数回に分ける必要があります。  
ちなみに2008年は全体で28,000件、4月は2,335件でした。

-   TID カンマ区切り。未指定の場合すべて
-   ChID カンマ区切り。未指定の場合すべて
-   StTime LastUpdateの指定方法と同じ
    -   「20090401\_000000-」と指定したら「2009-04-01 23:55～00:05」のデータは取得されないので注意
-   Range
    -   「20090401\_000000-20090402\_000000」の形式で指定する。LastUpdateと違い、必ず開始と終了を指定する
    -   「Range0 < EdTime AND StTime < Range1」の検索をする (しょぼいカレンダーは1番組が24時間以下であることを前提に最適化されているので、もしも24時間以上の番組が登録されていたら検索から漏れる)
-   Count カンマ区切り。未指定の場合すべて
-   LastUpdate 日付の範囲。未指定の場合すべて
-   Fields 出力するフィールド。未指定の場合すべて
-   JOIN
    -   JOIN=SubTitles でSTSubTitleフィールドが追加される(サブタイトルテーブルの内容が結合される)
-   PID カンマ区切り。未指定の場合すべて

## 注意

番組表ではサブタイトルが表示されているのに、db.phpの結果のSubTitleが空になっていることがあります。  
番組表と同じサブタイトルを表示するためには、別途サブタイトルテーブルからTIDとCountで検索するか、
JOIN=SubTitleパラメータを追加してSTSubTitleを利用します。  
サブタイトルテーブルはタイトルデータのSubTitlesをパースして生成されています。  
このため、サブタイトルが修正されても放送時間データのLastUpdateは更新されません。

## チャンネルデータの取得 (ChLookup)

-   ChID
-   LastUpdate

### チャンネルグループデータの取得 (ChGroupLookup)

-   ChGID
-   LastUpdate

## サブタイトルデータの取得

-   STID
-   TID
-   Count

## タイトルページのページビュー取得 (TitleViewCount)

## タイトルのポイントランキング履歴取得 (TitleRankHistory) 2020/02/06廃止

## タイトルのポイント履歴取得 (TitlePointHistory)

## タイトルのポイントランキングの上位を取得 (TitlePointTop)

## CSVで出力する

fmt=csv パラメータをつけると出力がCSVになります。  
現在対応しているのは以下のものだけです。

-   TitleLookup
-   ChLookup
-   ChGroupLookup
