---
title: json.php
---

## json.php

- 内部的に使ったりしてるjsonのメモ書き
- とつぜん仕様変更したり使えなくなったりするかもしれないけど、そうなったらごめんなさい
- いきあたりばったりで追加、変更してます

## 使い方

- http://cal.syoboi.jp/json.php
- パラメータ
|Req|コマンド|その他|
|---|---|---|
|callback|コールバックする関数|オプション|
|start|"YYYY-MM-DD" で日付、/^-(\\d+)d$/ でn日前| |
|days|startからの日数(1～32)| |
|TID| | |
|PID| | |
|ChID| | |
|Count| | |

コマンドは順番に実行される。  
ProgramByのあとにじっこうTitle*が実行されるときは、ProgramByの結果のTIDが自動的に指定され、SubTitlesが実行されるときは

## コマンド パラメータ (オプション)

TitleMedium、TitleLarge、TitleFullは、次の共通項目を返します。

`TID`, `Title`, `ShortTitle`, `TitleYomi`, `TitleEN`, `Cat`, `FirstCh`, `FirstYear`, `FirstMonth`, `FirstEndYear`, `FirstEndMonth`, `TitleFlag`

各コマンドの追加項目は次のとおりです。

- TitleMedium TID
    - 共通項目に加えて、Links
    - Linksはタイトルのコメントから抽出したリンク情報
- TitleLarge TID
    - 共通項目に加えて、Keywords, UserPoint, UserPointRank, TitleViewCount
        - だいたい60KBくらい(2007-10-23現在)
- TitleFull TID
    - 共通項目に加えて、Keywords, UserPoint, UserPointRank, TitleViewCount, Comment, SubTitles
        - だいたい5MBくらい(2007-10-23現在)
- ProgramByPID PID (TID, ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle2,ProgComment,ConfFlag
- ProgramByCount TID, Count (ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle2,ProgComment,ConfFlag
- ProgramByDate start, days (TID, ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle2,ProgComment,ConfFlag
- SubTitles TID, Count
- ChFilter
- TitleSearch
    - ヘッダーの検索窓で使用している検索機能。ヒットした番組と直近の放送予定が取得できる
    - json?Req=TitleSearch&Search=%E3%81%B7%E3%82%8A&Limit=15

## ProgramBy系の出力について

ProgramByPID、ProgramByCount、ProgramByDateの`SubTitle2`は、放送時間データの個別のサブタイトルです。タイトル・話数ごとの共通のサブタイトルは、`Req=SubTitles`で取得してください。ProgramBy系の結果には`SubTitle`は含まれません。

`Req=SubTitles`の結果は、`SubTitles[TID][Count]`をキーにサブタイトルを取得できる構造です。

`ProgComment`は放送時間データのコメントです。`ConfFlag`はユーザー設定に関する値で、ユーザー情報を取得する条件を満たさない場合は`null`になります。

## 変更履歴

- 2009-06-25
    - ProgramBy* でTIDとChIDが使えるように
    - ProgramBy* の結果のCountが次のリクエストのパラメータになるように
    - Start パラメータで /-(\\d)d/ の形式のとき現在時刻からさかのぼった日付を設定できるように
    - Days 最大値を22から32に変更
- 2008-11-18
    - ChIDFilter
    - Daysで21日まで許可
- 2007-10-23
    - TitleFullを追加
- 2007-10-18
    - TitleLargeを追加
    - TitleMedium, TitleLargeでTIDを指定しない場合、すべてのタイトルを返すように
- 2007-10-17
    - callbackの指定ができるように(JSONPに)
- 2007-09-21
    - つくった
