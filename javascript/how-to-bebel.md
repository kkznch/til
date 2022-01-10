# How to Babel

公式サイトを参考に進める。
[What is Babel?](https://babeljs.io/docs/en/)

学習用リポジトリは以下の通り。
[学習用リポジトリ](https://github.com/kkznch/learn-mini-react)

## 簡単な構成でbabelを使ってトランスパイルする
以下のコマンドを実行し、トランスパイルに必要なパッケージをインストールする。
```shell
> yarn add -D @babel/core @babel/cli @babel/preset-env                                  
```

以下の内容でbabel設定ファイルを作成する。
`corejs` プロパティを指定する際は、対応するバージョンのcorejsパッケージをインストールする必要があるらしいが、`@babel/preset-env` の依存パッケージに `core-js-compat` が含まれているため、明示的にインストールする必要はなさそう。
```js:babel.config.js
module.exports = {
  presets: [
    [
      "@babel/preset-env",
      {
        targets: {
          edge: "17",
          firefox: "60",
          chrome: "67",
          safari: "11.1",
        },
        useBuiltIns: "usage",
        corejs: "3.6.5",
      },
    ],
  ],
}
```

以下の内容でトランスパイル対象となるファイルを作成する。
```js:index.js
const sayHello = () => {
  console.log("Hello, world.");
}

sayHello();
```

babelコマンドを実行し、トランスパイルする。
```shell
> npx babel index.js --out-dir dist
```

このとき、 `dist` フォルダにトランスパイルされたファイルが出力されることを確認できる。
babel設定ファイルに記述したtargetsのバージョン次第で、トランスパイルの出力内容が変わる（Arrow Functionsに対応していないブラウザのために、Arrow FunctionsがFunctionに変わる）。


## babelのパッケージ
### @babel/core
https://babeljs.io/docs/en/babel-core.html

babelの本体。
入力としてJSのコードを受け取り、ASTに変換し、何らかの変換処理でASTを変換し、出力として再度JSコードを吐き出す。

### @babel/cli
https://babeljs.io/docs/en/babel-cli

babelをCLIから実行するためのパッケージ。

`--out-dir` オプションを付けて出力先のディレクトリを指定したり、 `--plugins` や `--presets` オプションを付けてプラグイン、プリセットの指定ができる。
また、 `--watch` または `-w` オプションをつけて実行することで、ファイルの変更を検知して変換を行ってくれる。

### @babel/preset-env  
https://babeljs.io/docs/en/babel-preset-env

対応ブウラウザなどの大雑把な情報を元に、必要なプラグインを自動で選択して、最新の ES6+ を動く状態にしてくれるプラグイン。

> これらのデータソースを活用して、サポートされているターゲット環境のどのバージョンがJavaScript構文またはブラウザー機能のサポートを取得したか、およびそれらの構文と機能のBabel変換プラグインとcore-jsポリフィルへのマッピングを維持します。

Browserslistと組み合わせ、シェア率がn%以上のブラウザに対応する、といった設定もできる。


## PluginsとPresets
### Plugins
コードへの変換を実行する方法をBabelに指示するプログラム。

### Presets
プラグインの組み合わせをまとめて提供する。


## Babel設定ファイルについて
https://babeljs.io/docs/en/configuration

プロジェクト全体に設定を反映したい場合は babel.config.json で、フォルダに個別に設定を適用したい場合は .babelrc.json と使い分ける。

環境に合わせるなど、動的に設定を変更したい場合は babel.config.js といったようにJSの形式で設定を記述できる。



## 参考
- [@babel/preset-env (Babel 7)をハンズオンでちゃんと理解する](https://zenn.dev/sa2knight/articles/67f6f5cc4ed5e26e391c)
- [Babel7.4で非推奨になったbabel/polyfillの代替手段と設定方法](https://aloerina01.github.io/blog/2019-06-21-1)