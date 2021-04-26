---
title: rss2.php 
---

# rss.php

## rss.php との違い

- トップページの番組表に使われている処理と同じ物が使われている
    - アップロードしたtsvデータが取得可能
    - アップロードした自分の録画予定が取得可能
    - 共有された録画予定が取得可能
    - 最適化されていて速い(負荷が低い)
- RSSのバージョンが2.0 (rss.phpは1.0)
- 時間の指定方法を分単位
- 出力行数の制限なし (ただし取得範囲は7日)

## パラメータ

- start
    - YYYYMMDDhhmm 開始時間
    - 未指定の場合現在時刻
- end
    - YYYYMMDDhhmm 終了時間
    - 未指定の場合(start+1日)
- days
    - 日数(1～14)
    - これを指定する場合、endは指定しないでください
- titlefmt
    - 別途
- usr
    - ユーザID
- filter
    - 0:そのまま
    - 1:強調フラグのみ
    - 3:半透明を除く
    - usr指定時のみ有効
- alt
    - rss: RSS2.0
    - ical: iCalendar
    - json: JSON/JSONP(rss.phpと違って、番組表として処理される前の生のデータ)
- callback
    - jsonのcallback先の関数名
    - alt=jsonの時のみ有効
- usch
    - 1: ユーザによってアップロードされたスケジュールを含む
- ssch
    - 1: ユーザによって共有されたスケジュールを含める

## titlefmt

rss.php とほぼ同じですが、以下のものが追加されています。

- usch=1の場合のみ有効
    - DevName
        - 予約しているデバイス名
    - DevTitle
        - デバイスによって予約されている予約名
    - DevColor
        - デバイスに設定された色(#RRGGBBか#RGB)
- ssch=1の場合のみ有効
    - Followers
        - 予約人数

rss.php と同じもの。

- TID
    - TID(番組ごとのID)
- PID
    - PID(放送時間ごとのID)
- Title
    - 完全なタイトル
- ShortTitle
    - 短いタイトル
- ChName
    - チャンネル名
- ChiEPGName
    - iEPG用のチャンネル名(存在しない場合はChNameと同内容)
- ChID
    - チャンネルID
- ChGID
    - チャンネルグループID
- OffsetA
    - 開始時間のずれ (例:+30)
- OffsetB
    - 開始時間のずれ (例:▼30)
- Count
    - 回数
- SubTitleA
    - サブタイトル
- SubTitleB
    - 回数+サブタイトル (例:#302 「笑ってユルして・・・派出所全員あっはっは」)
- Mark
    - マーク (例:【新】)
- MarkW
    - 警告マーク (例:【！】)
- Flag
    - PIDに設定されたフラグの数値
        - 1:注
        - 2:新
        - 4:終
        - 8:再
- FlagW
    - 警告フラグの数値
        - 0:なし
        - 1:先週無かったか時間が違う
- StTime
    - 開始時間 (例:12/05 19:00)
- EdTime
    - 終了時間 (例:19:30)
- StTimeU
    - 開始時間 (Unix Epoch)
- EdTimeU
    - 終了時間 (Unix Epoch)
- Revision
    - 修正回数
- LastUpdateU
    - 更新時間 (Unix Epoch)
- ConfFlag
    - ユーザ設定の値
- Cat
    - カテゴリ値
