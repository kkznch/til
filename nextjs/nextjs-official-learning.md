# Next.js official learning

作業用リポジトリ

https://github.com/kkznch/learn-nextjs-tutorial-basics

## Pre-rendering and Data Fetching
### Next.js は Pre-rendering に対応してるよ
Next.js は Pre-rendering に対応しており、ページにアクセスした際は静的なページが返されるようになっている。そのため、ブラウザの JavaScript をオフにした状態でページにアクセスしてもページは表示される。

一方、素の React.js は No Pre-rendering のため、ブラウザの JavaScript をオフにしている状態でページにアクセスしても何も表示されない。

### 静的ページ生成時のデータ取得のおともに
`getStaticProps` 関数を定義しておくと、静的ページ生成時（ビルド時）に `getStaticProps` 関数が実行され、その結果が Home コンポーネントの props として渡される。

```js:index.js
export async function getStaticProps() {
  // 例えば、ここらへんにデータ取得する処理書く（DBアクセス、外部APIなど）
  return {
    props: {
        hoge: 'ほげほげ',
    }
  }
}

export default function Home ({ hoge }) { 
  
  return {
      <></>
  }
}
```

development (npm run dev or yarn dev) の場合は `getStaticProps` はリクエストする度に実行される。
production の場合はビルド時のみ実行されるが、 `getStaticPaths` から返される `fallback` を用いることでカスタマイズできるらしい。

### SSR時のデータ取得のおともに
`getServerSideProps` 関数を定義するといい。
`context` にはリクエストに関するパラメータなどが入ってるっぽい。

```js
export async function getServerSideProps(context) {
  return {
    props: {
      // props for your component
    }
  }
}
```

## Dynamic Routes
### getStaticPaths で静的パスの生成
`getStaticProps` を使用して動的ルートにアクセスする際、以下のように `getStaticPaths` で指定したパスを静的にプリレンダリングしておくことができる。
SPAではなくSSGの際に使用するもので、予めどういったパスにどういったコンテンツが存在するか、を定義するために使うものだはず。

```js
export async function getStaticPaths() {
  return {
    paths: [
      { 
        params: {
          id: 'hoge',
        }
      },
    ],
    fallback: true,
  };
}
```

`fallback` プロパティについては以下を参照するとよい。

[The fallback key (required)](https://nextjs.org/docs/basic-features/data-fetching#the-fallback-key-required)


## 参考
- [Next.js](https://nextjs.org/learn/basics/create-nextjs-app)

