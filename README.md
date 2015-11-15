# textlint-rule-no-doubled-joshi [![Build Status](https://travis-ci.org/azu/textlint-rule-no-doubled-joshi.svg?branch=master)](https://travis-ci.org/azu/textlint-rule-no-doubled-joshi)

文中に同じ助詞が複数出てくるのをチェックする[textlint](https://github.com/textlint/textlint "textlint")ルールです。

例)

> 材料不足で代替素材で製品を作った。

**で** という助詞が一文で複数回でてきている。


## Installation

    npm install textlint-rule-no-doubled-joshi

Require: textlint 5.0 >=

## Usage

### Options

`.textlintrc` options.

```js
{
    "rules": {
        "no-doubled-joshi": {
            // 助詞のtoken同士の距離が2以下ならエラー
            "min_interval" : 2,
            // 例外を許可するかどうか
            "strict": true
        }
    }
}
```

- `min_interval` : 助詞の最低間隔値
    - 指定した間隔値以下で同じ助詞が出現した場合エラーが出力されます。
    

> 私**は**彼**は**好き

この場合の、**は**と**は**の間隔値は1

> 既存**の**文章**の**修正

この場合の、**の**と**の**の間隔値は2

## Tests

    npm test

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## License

MIT

## Reference

- [Doubled Joshi Validator · Issue #460 · redpen-cc/redpen](https://github.com/redpen-cc/redpen/issues/460 "Doubled Joshi Validator · Issue #460 · redpen-cc/redpen")
- [事象の構造から見る二重デ格構文の発生 ](https://www.ninjal.ac.jp/event/specialists/project-meeting/files/JCLWorkshop_no6_papers/JCLWorkshop_No6_01.pdf "JCLWorkshop_No6_01.pdf")
- [第８回：読みやすさへの工夫 3（てにおは助詞） - たくみの匠](http://www.asca-co.com/takumi/2010/07/3.html "第８回：読みやすさへの工夫 3（てにおは助詞） - たくみの匠")
- [(Microsoft Word - JCLWorkshop2013_2\214\303\213{.doc) - JCLWorkshop_No3_02.pdf](https://www.ninjal.ac.jp/event/specialists/project-meeting/files/JCLWorkshop_no3_papers/JCLWorkshop_No3_02.pdf "(Microsoft Word - JCLWorkshop2013_2\214\303\213{.doc) - JCLWorkshop_No3_02.pdf")
- [助詞の連続使用を避け分かりやすい文章を書こう！ - 有限な時間の果てに](http://popoon.hatenablog.com/entry/2014/07/11/232057 "助詞の連続使用を避け分かりやすい文章を書こう！ - 有限な時間の果てに")
- [作文入門](http://www.slideshare.net/takahi-i/ss-13429892 "作文入門")

## 判定処理

ある助詞(かつ品詞細分類)が一致するものが、一定最低間隔値(距離)以下に書かれている場合を検出する。

[元ネタ](https://github.com/redpen-cc/redpen/issues/460 "Doubled Joshi Validator · Issue #460 · redpen-cc/redpen")は助詞が1文(センテンス)に2回以上でてきた際にエラーとしてる。

少し厳しすぎると感じたので、1文(センテンス)ではなく最低間隔値(距離)という概念を導入した

> この書籍はJavaScriptのライブラリやツールにおけるプラグインアーキテクチャを見ていく事を目的としたものです

この場合 "を" が最低間隔値2で並んでいるためエラーとするべき。

- [kuromoji.js demo](http://takuyaa.github.io/kuromoji.js/demo/tokenize.html "kuromoji.js demo")

## 例外

以下の項目については、曖昧性があるため助詞が連続していてもデフォルトではエラーとして扱わない。

設定が `{ strict: true }` ならばエラーとするが、デフォルトでは`{ strict: false }` となっている。

#### 助詞:連体化 "の"

"の" の重なりは例外として許可する。

- [第８回：読みやすさへの工夫 3（てにおは助詞） - たくみの匠](http://www.asca-co.com/takumi/2010/07/3.html "第８回：読みやすさへの工夫 3（てにおは助詞） - たくみの匠")
- [作文入門](http://www.slideshare.net/takahi-i/ss-13429892 "作文入門")
    - "の" の消し方について

#### 助詞:格助詞 "を"

> オブジェクトを返す関数を公開する

"を" の重なりは例外として許可する。
