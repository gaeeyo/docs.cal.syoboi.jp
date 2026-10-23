---
title: json.php
date: 2026-10-23T23:11:01+09:00
---

## json.php

- 内部的に使ったりしてるjsonのメモ書き
- とつぜん仕様変更したり使えなくなったりするかもしれないけど、そうなったらごめんなさい
- いきあたりばったりで追加、変更してます

## 使い方

- https://cal.syoboi.jp/json.php
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

`Req`にはコマンドをカンマ区切りで指定でき、指定した順番に実行されます。

ProgramBy系のコマンドは、`TID`が未指定の場合は結果のタイトルID一覧を、`Count`が未指定の場合は結果の話数一覧を、後続コマンドのパラメータに設定します。指定済みのパラメータは上書きしません。空文字を指定した場合も、指定済みとして扱います。

例えば、`Req=ProgramByPID,TitleMedium,SubTitles&PID=12345`と指定すると、その放送時間データと、対応するタイトル情報・サブタイトルをまとめて取得できます。

## サービス内での利用例

### ヘッダーの検索候補

ヘッダーの検索窓では、入力したキーワードを`TitleSearch`に渡し、検索候補と直近の放送予定を表示しています。

```text
/json.php?Req=TitleSearch&Search=ぷり&Limit=15
```

`Search`は検索するキーワードです。実際にURLに含める場合はURLエンコードしてください。返却された`Titles`からタイトル名などを取り出し、放送予定の`Programs`が含まれている場合は、その日時やチャンネル名も表示します。

### 番組表の話数をクリックしたときのポップアップ

番組表の話数をクリックすると、同じタイトル・話数の放送日一覧を表示します。このポップアップでは、複数のコマンドを1回のリクエストにまとめています。

```text
/json.php?Req=ProgramByCount,TitleMedium,ChFilter,SubTitles,UPS&UserInfo=1&TID=1234&Count=1
```

`TID=1234`はタイトルID、`Count=1`は話数の例です。実際には、クリックした番組の値を指定します。

| コマンド | ポップアップでの用途 |
| --- | --- |
| ProgramByCount | 同じタイトル・話数の放送日時とチャンネル名を取得 |
| TitleMedium | タイトル名と関連リンクを取得 |
| ChFilter | ユーザーのチャンネル設定を取得し、表示に反映 |
| SubTitles | その話数の共通のサブタイトルを取得 |
| UPS | その話数の「チェック」「見逃し」の状態を取得 |

`UserInfo=1`は、放送データにユーザーの強調設定（`ConfFlag`）を含めるための指定です。この例では`ChFilter`も指定するため、自動ログインの確認が有効になります。ユーザーに関する情報はログイン状態に依存します。

このように、放送データ、タイトル情報、サブタイトルは別々に取得し、画面で組み合わせて使います。この例では`TID`と`Count`を明示しているため、各コマンドはその値を使います。

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
