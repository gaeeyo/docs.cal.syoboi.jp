---
title: プラグインスクリプト (廃止予定)
---

**お知らせ (2021-03-06)**

**この機能は近日中に廃止予定です。**

## プラグインスクリプトとは

設定ページでスクリプト(JavaScript)のURLを指定すると、しょぼいカレンダーで任意のスクリプトを実行できます。

設定はこちらから。(この機能はログインしなければ使えません)

-   [http://cal.syoboi.jp/uc](http://cal.syoboi.jp/uc)





しょぼいカレンダーの仕様変更により突然使えなくなることがあります。

URLは http:// から始まっている必要があるので、一時的にスクリプトを利用したくない場合は ttp:// とすると良いかもしれません。



## Twitterでつぶやく

```
http://cal.syoboi.jp/plugin_script/twitter.js
```

headとfmtパラメータが使えます。

headパラメータ



```
http://cal.syoboi.jp/plugin_script/twitter.js?head=見る:
```



とすると「<b>見る:</b> (番組名) #(番号) 「(サブタイトル)」 at (チャンネル)」のようになります。

fmtパラメータ

デフォルトは「fmt=count subtitle chname」です。(+は+記号ではなくて空白



```
http://cal.syoboi.jp/plugin_script/twitter.js?fmt=count
```



とすると、「(番組名) #(番号)」になります。(サブタイトルとチャンネルが省略されている)



コピペ用テキスト表示



```
http://cal.syoboi.jp/plugin_script/text.js
```





## はてなスター設置

2つのスクリプトを、順番どおりに記入する必要があります。



```
http://s.hatena.ne.jp/js/HatenaStar.js
```

```
http://cal.syoboi.jp/plugin_script/hatenastar.js
```



![](fidgae20090628213349pimage.png)





## またアニメ見てる

見ているアニメをtwitterでつぶやく「[またアニメ見てる](http://mataanimemitetari.shimasu.net/)」と似た書式でつぶやきます。(※適当に似せただけなのでまずい部分があるかも)


```
http://cal.syoboi.jp/plugin_script/mataanimemiteru.js
```



![](fidgae20090628213159pimage.png)

![](fidgae20090628213040pimage.png)
