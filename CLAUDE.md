# カメラ買取比較記事LP

## ステータス: テスト版デプロイ済み → デザイン改善中
- URL: https://ad-kaitori-camera.vercel.app
- GitHub: https://github.com/ishibe-ai/ad-kaitori-camera

## 概要
低用量ピルクリニック比較記事（zenclinic.jp/media_lp/pill/）の構成・デザインを流用し、カメラ買取ジャンルで横展開テスト中。

## 案件情報
| 順位 | サービス | 報酬 | CVR | URL |
|------|---------|------|-----|-----|
| 1位 | 福ちゃん（REGATE） | 7,000-7,500円 | 4% | https://fuku-chan.jp/camera/?page=asp |
| 2位 | カメラの買取屋さん（GRACE） | 5,000円 | 2% | http://camerakaitori.jp/lp_afi/?argument=rYCPokjR&dmai=a6229706de9b56 |
| 3位 | JUSTY | 3,500円 | - | https://justy-consul.com/camera/ |

## 技術構成
- 静的HTML + jQuery + Font Awesome
- CSS: 元のzenclinic.jpのapplication.cssをインライン化
- 画像: NanoBanana 2 (gemini-3.1-flash-image-preview) + NanoBanana Pro (nano-banana-pro-preview) で生成 + 各社LPから取得 + フリー素材
- Gemini APIキー: `~/ad/.env` に保存

## 画像生成で使用したAPI
- gemini-3.1-flash-image-preview (NanoBanana 2): FV、見出し6枚、選び方イラスト3枚
- nano-banana-pro-preview (NanoBanana Pro): ファビコン、メリット4枚
- リファレンス画像を入力として渡すと品質が上がる

## 残課題（優先度順）
1. テキスト内容の精査（案件情報の正確性、コピーの自然さ）
2. モバイルレスポンシブの確認・調整
3. アフィリエイトリンクの動作確認
4. GTM設置
5. Google広告アカウント設定
6. 本番用ドメイン検討（現在vercel.app）

## 元テンプレート
- 低用量ピルLP分析: `~/ad/lp-reference/低用量ピルクリニック_比較記事.html`
- 元HTMLソース: `/tmp/pill-source.html` + `/tmp/pill-source.css`（セッション間で消える）
- 永続化が必要なら `lp-reference/` にテンプレートHTMLとして保存する

## ディレクトリ構成
```
ad-kaitori-camera/
├── CLAUDE.md          ← このファイル
├── index.html         ← メインLP
├── company.html       ← 運営者情報
├── camera-assets/     ← 画像素材
│   ├── fv-v2.jpg      ← FVバナー（NB2生成）
│   ├── heading-*.png  ← 見出し画像（NB2生成、背景透過済み）
│   ├── merit1-4.jpg   ← メリットイラスト（NB Pro生成）
│   ├── choice-v2-*.png ← 選び方イラスト（NB2生成、背景透過済み）
│   ├── fukuchan-*.webp/svg ← 福ちゃん素材
│   ├── kaitoriyasan-*.png  ← カメラの買取屋さん素材
│   ├── justy-*.webp/png    ← JUSTY素材
│   └── score*.png, rank*.png等 ← 汎用UI素材
└── .vercel/
```
