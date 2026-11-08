# 拉麺喫茶HOME 8823 公式サイト

GitHub Pages で公開する静的サイトです。ビルド不要、このフォルダの中身をそのままリポジトリに置けば動きます。

## ファイル構成

```
index.html              トップページ
menu.html               メニューページ（おしながき＋喫茶メニュー）
style.css               2ページ共通のスタイル（デザインの変更はここ）
404.html                ページが見つからないとき用
menu-ramen.pdf          印刷用おしながき
menu-cafe.pdf           印刷用喫茶メニュー
favicon-32.png          ブラウザのタブアイコン
apple-touch-icon.png    スマホのホーム画面アイコン
robots.txt              検索エンジン向け設定（仮公開中は全拒否）
sitemap.xml             サイトマップ（本公開時に使用）
.nojekyll               GitHub Pages の Jekyll 処理を無効化
hero-ramen.webp         トップの全面メインビジュアル（PC用・横長）
hero-ramen-sp.webp      同上（スマホ用・縦長）
storefront.jpg          「お店について」の外観写真（高解像度版に差し替え推奨）
ramen-shoyu.jpg         中華そば（メニューPDFから切り出し）
ramen-shio.jpg          塩中華そば（同上）
kids-room_temp.jpg      ★仮画像：2階キッズルーム
private-room_temp.jpg   ★仮画像：奥の個室
logo-navy.png / logo-cream.png
ogp.jpg                 SNSでシェアされたときの画像（1200×630）
```

## ページ構成

- **トップ（index.html）**：全面のラーメン写真にロゴとキャッチを重ねたメインビジュアル → 営業時間の帯 → お店について（外観・キッズルーム・個室） → 食後の喫茶セットの帯 → 人気の3品とメニューページへの導線 → 店舗情報・地図
  - トップだけヘッダーを写真の上に重ねた作りにしているため、紙メニュー風の二重枠は使っていません（menu.html には残しています）。
- **メニュー（menu.html）**：おしながき（ラーメン・トッピング・ご飯もの・セット・サイド・お子様・定食）→ 喫茶メニュー → 印刷用PDFへのリンク

トップを短く保ち、細かい価格はメニューページにまとめています。`/menu.html` は単独のURLなので、InstagramやGoogleビジネスプロフィールからメニューへ直接リンクできます。

## 1. 仮公開（今すぐできる）

1. GitHub で新しいリポジトリを作成（例：`home8823`）。Public にする。
2. このフォルダの中身をすべてアップロードして main ブランチにコミット。
3. リポジトリの Settings → Pages → Source を「Deploy from a branch」、Branch を `main` / `/ (root)` にして Save。
4. 数分後に `https://<ユーザー名>.github.io/home8823/` で表示される。

仮公開中は `noindex` と `robots.txt` で検索に出ないようにしてあります。
※ 404.html はドメイン直下を前提にしているため、仮URLの間は404ページのロゴが表示されません（独自ドメイン設定後は正常）。

## 2. ドメイン取得後にやること（GitHub公式ドキュメントの推奨順）

参考：https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

**順番が大事です。DNSを設定する前に、必ずGitHub側にドメインを登録してください。** 逆にすると、第三者がそのドメインでサイトを公開できてしまうリスクがあります。

1. **ドメインを検証する**：アカウント（またはOrganization）の Settings → Pages → Add a domain にドメインを入力 → 表示されたTXTレコードをDNSに追加 → Verify。
2. **リポジトリに登録する**：リポジトリの Settings → Pages → Custom domain にドメイン（例：`home8823.com`）を入力して Save。ルートに `CNAME` ファイルが自動でコミットされる。
3. **DNSを設定する**（ドメイン会社の管理画面）。先に、ドメイン会社が自動で入れている既定のA/CNAMEレコード（駐車ページ用など）を削除してから追加する。

| 種類 | ホスト名 | 値 |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | `<ユーザー名またはOrganization名>.github.io`（リポジトリ名は付けない） |

- ワイルドカード（`*.home8823.com`）のレコードは作らない（乗っ取りの原因になる）。
- `home8823.com` と `www.home8823.com` の両方を設定しておけば、GitHubが自動でリダイレクトしてくれる。
- 反映には最大24時間かかる。

4. **HTTPSを有効にする**：Settings → Pages の「Enforce HTTPS」にチェック。選べるようになるまで最大24時間かかる。

## 3. 本公開チェックリスト

- [ ] `__DOMAIN__` をすべて実際のドメインに置換（index.html 6か所、menu.html 3か所、robots.txt、sitemap.xml）
- [ ] index.html と menu.html の `<meta name="robots" content="noindex, nofollow">` の行を削除（各1行）
- [ ] robots.txt を以下に書き換え
      ```
      User-agent: *
      Allow: /
      Sitemap: https://ドメイン/sitemap.xml
      ```
- [ ] **★仮画像2枚を実際の店内写真に差し替え**（他店の写真のまま公開しない）。ファイル名から `_temp` を外し、index.html の参照とコメントも更新
- [ ] storefront.jpg を横幅1600px以上の写真に差し替え
- [ ] 店舗情報の追加確認：電話番号、ラストオーダー、駐車場、SNS
- [ ] Google Search Console にドメインを登録し、sitemap.xml を送信
- [ ] Googleビジネスプロフィールの「ウェブサイト」欄にURLを登録

## 更新のしかた

- 価格・メニューの変更：**menu.html** の該当行を直接編集（価格は `<span class="p">` の中）。印刷用PDFも差し替える。中華そば・塩中華そばの値段はトップページ（index.html）にも出ているので、変わったときは両方直す。
- 写真の差し替え：同名ファイルを上書きアップロードすれば、HTMLの修正は不要。
- 見た目の調整（色・文字サイズ・余白）：style.css を直せば2ページとも変わる。
