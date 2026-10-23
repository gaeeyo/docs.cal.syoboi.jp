---
title: db.php
---

## db.php について

データベースからXMLでデータを出力するスクリプト。  
しょぼいカレンダー内では、Flashでグラフを表示しているところで使われています。

- https://cal.syoboi.jp/db.php

Commandパラメータに取得したいデータを指定します。(Command=TitleLookup のように指定する)  
基本的にdb.phpは、テーブルの生データをそのまま出力することを目的としています。

Fieldsパラメータには、各コマンドで指定可能なフィールド名をカンマ区切りで指定します。記載のないフィールド名を指定するとエラーになります。

## 処理結果とHTTPステータス

XMLレスポンスの`Result/Code`は、HTTPステータスコードとは別の処理結果コードです。

| Code | 意味 |
| --- | --- |
| 200 | 成功 |
| 400 | パラメータ不正 |
| 404 | 該当データなし |
| 500 | サーバー内部エラー |

`Result/Message`には、処理結果の説明が入ります。
`Result`の出力ではHTTPステータスを変更しないため、HTTPステータスが200でも、`Result/Code`がエラーを示す場合があります。XMLで結果を取得する場合は、`Result/Code`も確認してください。

一部の不正なリクエストでは、HTTP 400とプレーンテキストの`Bad Request`を返します。この場合、XMLの`Result`は返しません。

## タイトルデータの取得 (TitleLookup)

データベースに格納されているタイトルデータをそのまま出力します。

-   TID
    -   TIDの値を指定。カンマ区切りで最大100件指定可能。すべてのTIDを指定するときは \* を指定
        -   TID=1
        -   TID=1,2,3
        -   TID=\* (TIDのみを出力。レスポンスの肥大化を避けるため、全フィールドの出力から変更されました)
-   LastUpdate
    -   LastUpdateの範囲を指定。
        -   LastUpdate=20090421\_000000- ('2009-04-21 00:00:00' <= LastUpdate)
        -   LastUpdate=-20090421\_000000 (LastUpdate < '2009-04-21 00:00:00')
        -   LastUpdate=20090301\_000000-20090401\_000000 ('2009-03-01 00:00:00' <= LastUpdate AND LastUpdate < '2009-04-01 00:00:00')
-   Fields
    -   出力するフィールドをカンマ区切りで指定。未指定の場合はすべて出力。ただし、TID=\* の場合はTIDのみ指定可能
        -   Fields=TID (TIDだけを出力する)
        -   Fields=Title,Cat (TitleとCatを出力する)

Fieldsに指定可能な値:

`TID`, `LastUpdate`, `Title`, `ShortTitle`, `TitleYomi`, `TitleEN`, `Comment`, `Cat`, `TitleFlag`, `FirstYear`, `FirstMonth`, `FirstEndYear`, `FirstEndMonth`, `FirstCh`, `Keywords`, `UserPoint`, `UserPointRank`, `SubTitles`

ただし、TID=\* の場合は `TID` のみです。

## 使用例

-   全タイトルのID一覧を取得
    -   /db?Command=TitleLookup&TID=\*
    -   詳細は取得したTIDを最大100件ずつ指定して取得します
-   指定期間に更新されたタイトルのID一覧を取得
    -   /db?Command=TitleLookup&TID=\*&LastUpdate=20261001_000000-20261002_000000
    -   詳細は同様にTIDを指定して取得します
-   TID=1853 のタイトル情報を取得
    -   /db?Command=TitleLookup&TID=1853
-   タイトルの検索
    -   json.php を参照

最近の更新の検知には [titleinfo.xml](https://cal.syoboi.jp/titleinfo.xml) も利用できます。
過去7日以内に更新されたタイトルを更新日時の降順で最大500件返すRSSで、タイトル名・履歴ページへのリンク・更新日時を含みます。
詳細はリンクからTIDを得て取得してください。全件取得には使えず、7日以上取得を止めた場合や更新が500件を超えた場合は取りこぼすため、差分取得には上記のLastUpdate指定を利用してください。

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

Fieldsに指定可能な値:

`LastUpdate`, `PID`, `TID`, `StTime`, `StOffset`, `EdTime`, `Count`, `SubTitle`, `ProgComment`, `Flag`, `Deleted`, `Warn`, `ChID`, `Revision`

JOIN=SubTitlesを指定した場合は `STSubTitle` も指定可能です。`PID` はFieldsから省略しても出力されます。

## 注意

番組表ではサブタイトルが表示されているのに、db.phpの結果のSubTitleが空になっていることがあります。  
番組表と同じサブタイトルを表示するためには、別途サブタイトルテーブルからTIDとCountで検索するか、
JOIN=SubTitlesパラメータを追加してSTSubTitleを利用します。  
サブタイトルテーブルはタイトルデータのSubTitlesをパースして生成されています。  
このため、サブタイトルが修正されても放送時間データのLastUpdateは更新されません。

## チャンネルデータの取得 (ChLookup)

-   ChID
-   LastUpdate
-   Fields 出力するフィールドをカンマ区切りで指定。未指定の場合すべて

Fieldsに指定可能な値:

`LastUpdate`, `ChID`, `ChName`, `ChiEPGName`, `ChURL`, `ChEPGURL`, `ChComment`, `ChGID`, `ChNumber`

### チャンネルグループデータの取得 (ChGroupLookup)

-   ChGID
-   LastUpdate
-   Fields 出力するフィールドをカンマ区切りで指定。未指定の場合すべて

Fieldsに指定可能な値:

`LastUpdate`, `ChGID`, `ChGroupName`, `ChGroupComment`, `ChGroupOrder`

## タイトルページのページビュー取得 (TitleViewCount)

## タイトルのポイント履歴取得 (TitlePointHistory)

## タイトルのポイントランキングの上位を取得 (TitlePointTop)

## CSVで出力する

fmt=csv パラメータをつけると出力がCSVになります。  
現在対応しているのは以下のものだけです。

-   TitleLookup
-   ChLookup
-   ChGroupLookup
