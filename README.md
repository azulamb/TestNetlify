# Netlify のテスト

https://www.netlify.com/

GitHubのリポジトリをHTTPS+独自ドメインで公開できるサービス。
最近HTTPSじゃないと使えない技術が出てきたのと、無料でさくっとできるので試してみた。

https://lucid-noether-8668f5.netlify.com/page/test

## メモ

* サイトはリポジトリにPushしたときに行われる。
* ビルドコマンドもある程度叩けるらしい。
* 公開フォルダを設定し、そこを公開する。
    * 後述する `_redirects` は公開ディレクトリに置く。

## _redirects

特定の条件を満たしたURLをリダイレクトしてくれる……わけではない。
挙動は以下のようになっている。

* URLはそのまま
* _redirectsに書かれたファイルが読み込まれる

なので以下のような `_redirects` の場合、次のような挙動になる。

```
/page/* /index.html     200
```

* http://XXXX/
    * 普通にindex.htmlが表示される。
* http://XXXX/notfoundpage
    * 存在しないページはデフォルトの404が表示される。
* http://XXXX/page/test
    * エラーにはならずindex.htmlが表示される。
    * ただし、このindex.htmlは/page/以下にあるものとして振る舞うので、相対パスのファイルはすべてindex.htmlが返される。

SPAに非常に向いている挙動をしている。
