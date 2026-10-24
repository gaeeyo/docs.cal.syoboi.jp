---
title: データを取得する方法 
date: 2026-10-24T09:09:17+09:00
---

## HTML以外でデータを出力するもの一覧

- rss.php 番組表RSS
    - https://cal.syoboi.jp/rss.php (RSS 1.0/iCalendar/JSON)
- rss2.php 番組表RSS（アップロード・共有された録画予定にも対応）
    - https://cal.syoboi.jp/rss2.php (RSS 2.0/iCalendar/JSON)
- proginfo.xml 放送時間データの更新時間
    - https://cal.syoboi.jp/proginfo.xml (RSS 2.0)
- titleinfo.xml タイトルデータの更新時間
    - https://cal.syoboi.jp/titleinfo.xml (RSS 2.0)
- chinfo.xml チャンネルデータの更新時間
    - https://cal.syoboi.jp/chinfo.xml (RSS 2.0)
- db.php データいろいろ(実験的なもの)
    - https://cal.syoboi.jp/db.php
    - サンプル: https://cal.syoboi.jp/graph.php?src=Command%3DTitlePointHistory%26TID%3D491
- json.php データいろいろ(実験的なもの)
    - https://cal.syoboi.jp/json.php
    - サンプル: http://blog.livedoor.jp/gaeeyo/archives/361911.html
- ical.php 番組表をiCalendarで
    - https://cal.syoboi.jp/ical.php
    - 変わりにrss.phpが使えます
- rank 予約数のランキング
    - https://cal.syoboi.jp/reserve/rank?alt=json (テンプレートに渡されてるデータそのまま)
- しょぼいカレンダーグループのキーワードのRSS (ここのWiki)
    - https://syobocal.g.hatena.ne.jp/keywordlist?mode=rss (RSS 1.0)
- したらばの掲示板のRSS
    - https://jbbs.livedoor.jp/bbs/subject.cgi/anime/3083/rss (RSS 1.0)
