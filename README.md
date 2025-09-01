# HTML Meta Settings

## theme-color

SafariやAndroid版のChromeのアドレスバーの色を変えたりする。

意味があるかは、だいぶ怪しいものになっている。

- References

https://developer.mozilla.org/ja/docs/Web/HTML/Reference/Elements/meta/name/theme-color

## Favicon

### 行う処理

1. [Real Favicon Generator](https://realfavicongenerator.net/) でfaviconに関するあれこれを生成

2. 生成された画像群をダウンロードし、自分のウェブサイトのプロジェクトに追加

3. `site.webmanifest`を`manifest.json`にリネーム

4. タグを以下のように編集する

パスは自分のウェブサイトのプロジェクトに合わせて変更すること。

#### 編集前

**全体**

```html
<link rel="icon" type="image/png" href="/assets/favicon-96x96.png" sizes="96x96" />
<link rel="icon" type="image/svg+xml" href="/assets/favicon.svg" />
<link rel="shortcut icon" href="/assets/favicon.ico" />
<link rel="apple-touch-icon" sizes="180x180" href="/assets/apple-touch-icon.png" />
<link rel="manifest" href="/assets/site.webmanifest" />
```

#### 編集後

**3行目**

- before

```html
<link rel="shortcut icon" href="/assets/favicon.ico" />
```

- after

```html
<link rel="icon" href="/assets/favicon.ico" type="image/vnd.microsoft.icon" sizes="any" />
```

**5行目**

- before

```html
<link rel="manifest" href="/assets/site.webmanifest" />
```

- after

```html
<link rel="manifest" href="/assets/manifest.json" />
```

**全体**

```html
<link rel="icon" type="image/png" href="/assets/favicon-96x96.png" sizes="96x96" />
<link rel="icon" type="image/svg+xml" href="/assets/favicon.svg" />
<link rel="icon" href="/assets/favicon.ico" type="image/vnd.microsoft.icon" sizes="any" />
<link rel="apple-touch-icon" sizes="180x180" href="/assets/apple-touch-icon.png" />
<link rel="manifest" href="/assets/manifest.json" />
```

終了

- References

https://zenn.dev/toshihide2000/articles/a41031f1003cf2

### Faviconに関するあれこれ

Faviconに関するいろいろは、以下にまとめた。

基本的に以下のサイトを主軸に調査した。

https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html

#### svg画像によるfaviconの指定について (モダンブラウザ用のfavicon)

svg画像によるfaviconの指定は以下のように行う。

```html
<link rel="icon" href="/icon.svg" type="image/svg+xml">
```

- References

https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html

#### favicon.icoについて (レガシーブラウザ用のfavicon)

参考: svgアイコンのサポート状況

https://caniuse.com/link-icon-svg

もともとfaviconはマイクロソフトによって提案され、その後にマイクロソフトは`link`
要素によってfaviconを呼び出すサポートをした。しかし、W3Cの最初の勧告において、
次の3点が問題とされた。

- `rel="shortcut icon"`とする仕様について、半角スペースを含むため、2つの属性値として解釈され、ウェブブラウザを混乱させる。
- ICO形式にはIANAに登録されたMIMEタイプの割り当てがないため、多くのブラウザはfaviconとして指定されたファイルの種類を解析できない。
- `favicon.ico`にアクセスする方式では、特定のURIをこの用途に占有することになり、World Wide Webのアーキテクチャにそぐわない。

※ 2003年にICO形式が`image/vnd.microsoft.icon`としてIANAに登録されるまでは、MIMEタイプの割り当てがなかった。そのため、2003年以前では未登録トークンを`x-`で表す規則から`image/x-icon`を使われていた。

注釈で伸べた通り、MIMEタイプの問題は2003年に解決されている。
Mozillaがブラウザでのサポートをする際に`<link rel="icon" type="image/png" href="/path/image.png">`という形式を加え、`link`要素にるfaviconの重複指定が可能になった。これを皮切りに多くのブラウザがこの形式 (`rel="icon"`) をサポートするようになり、同様の書式で標準化された。

従って、以下のようにfaviconを設定するのが正しい。

```html
<link rel="icon" href="/favicon.ico" type="image/vnd.microsoft.icon" sizes="any">
```

- References

https://ja.wikipedia.org/wiki/ICO_(%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88)

https://ja.wikipedia.org/wiki/Favicon

https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html

#### Appleデバイス用の 180×180のPNG画像

iPhoneやiPadのホーム画面のショートカットアイコンとして使用される。
iOS 8以降では180x18の解像度の画像が必要になった。他のデザイスでは画像が縮小される。

※Appleのタッチアイコンは画像の周りに20pxのパディングを確保し、背景にも色を与えておくと、より見栄えが良くなるらしい。

```html
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

- References

https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html

#### PWA用のWebアプリケーションマニフェスト

使い方は、以下のReferencesのサイトを参照のこと。

- References

https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html

## Open Graph Protocol

Discordに貼るときにカードみたいなものが出るようになったりする。

Twitter Cardの設定も兼ねている。

- References

https://ogp.me/

## Twitter Card

Twitter (現: X) に投稿する際に、カード形式で表示されるようにするための設定。

画像やタイトル情報などのOpen Graph Protocolの設定を一部利用している。

画像容量を５MB以上だと表示されないので注意する。

「Card Validator」は機能していないので、実際のTwitterの下書きで確認する。

- References

https://unique1.co.jp/column/sns_operation/3033/
