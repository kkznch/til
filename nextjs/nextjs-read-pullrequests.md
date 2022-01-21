# Next.jsプルリク読み会
[vercel/next.js プルリク](https://github.com/vercel/next.js/pulls?q=is%3Apr+is%3Amerged)


# 2022/01/21(Fri)
- [fix(docs): Fix typo in Custom Build Id docs  area: documentation](https://github.com/vercel/next.js/pull/33515)
    - Documentのタイポ修正

- [Refactor base server to remove native dependencies  created-by: Next.js team type: next](https://github.com/vercel/next.js/pull/33499)
    - BaseServerに依存していたenv読み込み部分を抽象化し、継承先でenv読み込み部分を実装するようにした
    - NextNodeServerをランタイムに依存しないようにしたらしい
    - 大元のIssue https://github.com/vercel/next.js/issues/31506

- [Update with-linaria dependency  area: examples](https://github.com/vercel/next.js/pull/33487)
    - next-linaria ライブラリのバージョンアップに合わせてexampleのバージョンを修正した

- [feat(next-swc): Update swc  created-by: Next.js team type: next](https://github.com/vercel/next.js/pull/33485)
    - SWCのアップデートに合わせてバージョンとハッシュ修正した
    
- [Move static serving to next server  created-by: Next.js team type: next](https://github.com/vercel/next.js/pull/33475/files)
    - BaseServerからNode APIを剥がし、NextNodeServerで実装するようにした
    - 補足：NextServer と NextWebServer は別物で、NextWebServer は SSR Streamingに対応するためのものらしい
    - 大元のIssue https://github.com/vercel/next.js/issues/31506
    
- [Fix multiple calls to image onLoadingComplete()  created-by: Next.js team type: next](https://github.com/vercel/next.js/pull/33474)
    - onLoadingComplete を呼び出す際に何度も呼ばれるバグ修正
    - 元々は Set で状態を管理していたが、ref で管理されるようになってuseEffectなどの発火タイミングが修正されてるっぽい


