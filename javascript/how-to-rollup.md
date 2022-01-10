# How to rollup

## 簡単な構成で使ってみる
以下のコマンドでrollupをインストールする。
```shell
> yarn add -D rollup
```

以下の設定ファイルを用意する。
```js:rollup.config.js
export default {
  input: 'src/index.js',
  output: {
    file: 'dist/index.js',
    format: 'cjs',
  },
}
```

以下のコマンドを実行することでバンドルされる。
```shell
> npx rollup --config rollup.config.js
```


## 参考
- [rollup.js](https://rollupjs.org/guide/en/)
- [オリジナルのJavaScriptライブラリを作ろう](https://zenn.dev/manycicadas/books/b6f2d99b5208e9)
