# Differences between exports and module.exports

## 結論
> exports は module.exports のショートカットのようなもので、初期状態では exports は module.exports への参照です。
> module.exports に `module.exports.hoge = 'hogehoge'` のように関数や値を指定すると exports は module.exports の参照となり、 `module.exports = { hoge: 'hogehoge' }` のようにオブジェクトを指定すると exports は module.exports の参照ではなくなる。

> 関数と値を個別にエクスポートせず、1つだけをエクスポートするモジュールがある場合などは module.exports を使用するのがより一般的

## require
require はモジュールやファイルをインポートする関数。

```js
// 同じ階層のローカルファイル file1.js をインポート（拡張子は省略可能）
const foo = require('./file1');  

// ビルトインモジュールが検索された後、node_module ディレクトリにあるモジュール bar をインポート
const bar = require('bar');  
 
// ビルトインモジュール fs をインポート
const fs = require('fs');  
```

## exports
モジュールを他のプログラムで使用できるようにするには exports や module.exports を使う。
```js:user.js
// getName という関数を定義
const getName = () => { 
  return 'Foo';
};
 
// exports を使って他のファイルから getName をインポートできるようにする
exports.getName = getName;  
```

下記は関数とexportsをまとめたやつ。
```js:user.js
// exports.getName に関数を定義
exports.getName = () => { 
  return 'Foo';
};
```

上記で定義したuser.jsを使うときは以下のようにする。
```js
// user.js をインポート
const user = require('./user');  
 
// インポートした user の getName メソッドを使用
console.log(`ユーザ名： ${user.getName()}`); 
```

## module.exports
関数と値を個別にエクスポートせず、1つだけをエクスポートするモジュールがある場合などは module.exports を使用するのがより一般的。
```js:calc.js
module.exports = {
  add: (x, y) => {
    return x + y;
  },
 
  subtract: (x, y) => {
    return x - y;
  }
};
```

使うときは以下の通り。
```js
const calc = require('./calc');
 
const x = 200, y = 100;
 
console.log( `${x} + ${y} = ${calc.add(x, y)}`); 
console.log( `${x} - ${y} = ${calc.subtract(x, y)}`); 
```


## 参考
- [Node.js の exports と module.exports](https://www.webdesignleaves.com/pr/jquery/node-js-module-exports.html)