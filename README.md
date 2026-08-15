# portfolio

`alphajinsei.com` に置く、作ったものの一覧ページ。

作品を「関心の領域」で束ねて見せる。何を作ったかより、**何に興味があるか**が先に伝わることを狙っている。

## 構成

[index.html](index.html) の**1ファイルだけ**。ビルドも依存もない。
ブラウザで直接開けば、そのままの見た目で確認できる。

`old/` にデザイン検討時の他案と比較ページ（`compare.html`）を置いてあるが、
git では追跡していない。配色や構成を作り直したくなったときの参考用。

意図的にフレームワークを使っていない。ページが1枚で、記事のように量産する
性質のものではないので、ビルド工程を抱える割に合わない。ブラウザで開けば
必ず動く状態を優先している。（記事が増え続ける dia-logos は Astro のままでよい。）

## 編集のしかた

すべて `index.html` を直接編集する。

| やりたいこと | 操作 |
|---|---|
| 作品を足す | `<article class="product">` を1つコピーして書き換える |
| グループを足す | `<section class="group">` を1つコピーして書き換える |
| 分類を変える | `<article>` を別の `<section class="group">` に移す |
| 並び順を変える | `<section>` / `<article>` の順序を入れ替える |

分類は暫定でよい。空のグループは「書かなければ出ない」だけなので、
先に決めておく必要はない。

グループ見出しの通し番号（`<span class="group-num">01</span>`）は手で振る。
並べ替えたら振り直すこと。自動採番していないのは、そのためだけに JS を
持ち込む価値がないと判断したため。

### 公開状態のバッジ

`<span class="status">` を付けると出る。公開中のものには付けない。

```html
<span class="status">限定公開</span>   <!-- 認証あり -->
<span class="status">準備中</span>     <!-- 未公開 -->
```

未公開のものは `<h3>` を `<a>` にせず `<span>` にする。リンクにならず、
色も落ちて区別が付く。

```html
<h3><span>まだ公開していないもの</span></h3>
```

## デプロイ

Cloudflare Pages + GitHub 連携。

| 項目 | 値 |
|---|---|
| ビルドコマンド | （なし） |
| 出力ディレクトリ | `/`（リポジトリ直下） |
| 独自ドメイン | https://alphajinsei.com （apex） |
| Pages の既定URL | `portfolio-4zi.pages.dev` |

main に push すると自動でデプロイされる。

DNS は Cloudflare で管理している。仕組みの詳細は
[hoikuen/DNS_Management_Guide.md](../hoikuen/DNS_Management_Guide.md) に書いてある。

## 今後

- [ ] RL（Connect Four）— Flask + PyTorch なので OCI Always Free に立てる想定
- [ ] 保育園・API を叩くものの認証（限定公開の実装）
