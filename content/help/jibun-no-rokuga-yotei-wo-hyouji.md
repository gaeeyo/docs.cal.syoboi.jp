---
title: 自分の録画予定を表示
disableTableOfContents: true
---

### 「自分の録画予定を表示」について

利用している録画ソフトの予約リストをしょぼいカレンダーにアップロードすると、しょぼいカレンダー上で予約状況を確認できるようになります。

![](20100407231333.png)





### アップロードの方法

#### [TvRock](http://1st.geocities.jp/tvrock_web/)の場合

tvrockSchUploader.js を入手します。

-   [http://cal.syoboi.jp/client/tvrockSchUploader\_20100508.zip](http://cal.syoboi.jp/client/tvrockSchUploader_20100508.zip)

zipファイルから取り出した tvrockSchUploader.js を TvRock の作業ディレクトリにコピーします。

そして、TvRockのプロセスの設定に以下の行を追加します。



`MS:cscript tvrockSchUploader.js <user_id> <password> [epgurl] [slot]`



<user_id> と <password> には自分のものを設定してください。

たとえばユーザIDが「AB」でパスワードが「CD」の場合は以下のようにします。



`MS:cscript tvrockSchUploader.js AB CD`



\[epgurl\] は省略可能です。"http://192.168.0.5:8969/nobody/" のように指定しておくと、しょぼいカレンダーからTvRockのEPGの予約画面にリンクが張られます。

\[slot\] は省略可能です。





以上で、TvRock の予約リストが変更される度に自動的にアップロードされるようになります。

設定が間違っていなければTvRockで予約の状態を変更すると自動的にアップロードされ、しょぼいカレンダーに反映されます。





#### [PLUMAGE](http://seraphy.fam.cx/~seraphy/pg_all.html)の場合

TvRockの場合ほど易しくありません。まず plumageSchUploader.js を入手します。

-   [http://cal.syoboi.jp/client/plumageSchUploader\_20100401.zip](http://cal.syoboi.jp/client/plumageSchUploader_20100401.zip)

zipから取り出した plumageSchUploader.js を PLUMAGE.dat と同じディレクトリにコピーします。

コマンドプロンプトを開いて、スクリプトを実行します。スクリプトのパラメータは以下のようになっています。



`cscript plumageSchUploader.js <user_id> <password> [slot]`



<user_id> と <password> には自分のものを設定してください。ユーザIDが「AB」でパスワードが「CD」の場合、以下のようにします。



`cscript plumageSchUploader.js AB CD`



あとは、タスクスケジューラなどを使って、コマンドが定期的に実行されるようにします。





うまく動かすためには、PLUMAGEの予約一覧でチャンネル名が表示された状態になっている必要があります。リモコン信号を設定していない場合にも、「.」などを使ってチャンネル名が一覧で表示されるように設定します。



[![](jibun-no-rokuga-yotei-wo-hyouji/fidgae20100401213611pimage.png)](jibun-no-rokuga-yotei-wo-hyouji/fidgae20100401213611pimage.png)



[![](jibun-no-rokuga-yotei-wo-hyouji/fidgae20100401213612pimage.png)](jibun-no-rokuga-yotei-wo-hyouji/fidgae20100401213612pimage.png)





#### EDCB(EpgDataCap\_Bon)の場合

kkcald にアップロード機能が付いているようです。

-   [検索結果を時間軸で表示 kkcald](http://ueno.cool.ne.jp/kkcal/)





#### [foltia](http://www.dcc-jpl.com/soft/foltia/)の場合

perlスクリプトがあるようです。

-   [http://d.hatena.ne.jp/yuaaa/20100501/foltia\_sch\_upload](http://d.hatena.ne.jp/yuaaa/20100501/foltia_sch_upload)



#### その他のツールの場合

外部から予約リストが参照可能ならば、なんとかなるはずです。

アップロードに関する仕様は sch\_upload のページを確認してください。

-   [sch\_upload](../spec/sch_upload.html)





### アップロードしたデータを表示する

-   ログイン後の設定画面( http://cal.syoboi.jp/uc )で「自分の録画予定を表示」を「表示する」をクリックして、設定を保存します
-   表示されないときは..

-   設定ページでアップロードがされたかどうかを確認してください

-   http://cal.syoboi.jp/uc でアップロード時間を確認してください
-   アップロード時間が記録されているのに表示されない場合は、アップロードしたデータが異常である可能性があります

-   アップロードのコマンドを手打ちしてエラーがないことを確認してください

-   エラーがない場合何も表示されませんが、エラーがある場合何らかのエラーが表示されます



### 補足情報

-   読み込む順番

-   しょぼいカレンダーのデータ
-   ics(指定されていれば)
-   tsv(この機能でアップロードされるデータ)

-   しょぼいカレンダーのデータとの突き合わせ

-   開始時間とチャンネル名が一致しているかどうか**だけ**

-   どちらかの開始時間がずれている場合は別々の番組として表示されます
-   終了時間は考慮されませんので30分番組が突然1時間番組になっても一致していると見なされます(改善する予定)
-   チャンネル名は空白を削除して、英数字を半角にしてから一致するかどうか確認

-   「予約無効」に設定した番組が表示される(改善する予定)

