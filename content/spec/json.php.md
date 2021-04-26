---
title: json.php
---

# json.php

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
|Start|"YYYY-MM-DD" で日付、/^-(\\d+)d$/ でn日前| |
|Days|Startからの日数(1～32)| |
|TID| | |
|PID| | |
|ChID| | |
|Count| | |

コマンドは順番に実行される。  
ProgramByのあとにじっこうTitle*が実行されるときは、ProgramByの結果のTIDが自動的に指定され、SubTitlesが実行されるときは

## コマンド パラメータ (オプション)

- TitleMedium TID
    - Title, ShortTitle, Links
- TitleLarge TID
    - (TitleFullからCommentとSubTitlesを削除したもの)
        - だいたい60KBくらい(2007-10-23現在)
- TitleFull TID
    - Title, ShortTitle, TitleYomi, Comment, Cat, TitleFlag, FirstYear, FirstMonth, FirstCh, FirstEndYear, FirstEndMonth, Keywords, UserPoint, UserPointRank, TitleViewCount,Comment,SubTitles
        - だいたい5MBくらい(2007-10-23現在)
- ProgramByPID PID (TID, ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle,SubTitle2
- ProgramByCount TID, Count (ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle,SubTitle2
- ProgramByDate Start, Days (TID, ChID)
    - PID,TID,ChID,ChName,ChEPGURL,Count,StTime,EdTime,SubTitle,SubTitle2
- SubTitles TID, Count
- ChFilter
- ChIDFilter
- TitleSearch
    - ヘッダーの検索窓で使用している検索機能。ヒットした番組と直近の放送予定が取得できる
    - json?Req=TitleSearch&Search=%E3%81%B7%E3%82%8A&Limit=15

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
