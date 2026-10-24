---
title: プラグインスクリプト (廃止)
bookHidden: true
date: 2026-10-24T16:26:11+09:00
---

**この機能は廃止されました。以下は提供当時の説明です。**

## プラグインスクリプトとは

設定ページでスクリプト(JavaScript)のURLを指定すると、しょぼいカレンダーで任意のスクリプトを実行できます。

設定はこちらから。(この機能はログインしなければ使えません)

-   [https://cal.syoboi.jp/uc](https://cal.syoboi.jp/uc)





しょぼいカレンダーの仕様変更により突然使えなくなることがあります。

URLは http:// から始まっている必要があるので、一時的にスクリプトを利用したくない場合は ttp:// とすると良いかもしれません。



## Twitterでつぶやく

```
https://cal.syoboi.jp/plugin_script/twitter.js
```

headとfmtパラメータが使えます。

headパラメータ



```
https://cal.syoboi.jp/plugin_script/twitter.js?head=見る:
```



とすると「<b>見る:</b> (番組名) #(番号) 「(サブタイトル)」 at (チャンネル)」のようになります。

fmtパラメータ

デフォルトは「fmt=count subtitle chname」です。(+は+記号ではなくて空白



```
https://cal.syoboi.jp/plugin_script/twitter.js?fmt=count
```



とすると、「(番組名) #(番号)」になります。(サブタイトルとチャンネルが省略されている)



コピペ用テキスト表示



```
https://cal.syoboi.jp/plugin_script/text.js
```





## はてなスター設置

2つのスクリプトを、順番どおりに記入する必要があります。



```
https://s.hatena.ne.jp/js/HatenaStar.js
```

```
https://cal.syoboi.jp/plugin_script/hatenastar.js
```



![](fidgae20090628213349pimage.png)





## またアニメ見てる

見ているアニメをtwitterでつぶやく「[またアニメ見てる](http://mataanimemitetari.shimasu.net/)」と似た書式でつぶやきます。(※適当に似せただけなのでまずい部分があるかも)


```
https://cal.syoboi.jp/plugin_script/mataanimemiteru.js
```



![](fidgae20090628213159pimage.png)

![](fidgae20090628213040pimage.png)
