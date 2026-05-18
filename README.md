# 体調管理トラッカー

コロナ後遺症の症状と生活習慣の因果関係を記録・可視化する個人向けWebアプリです。

## 機能

- **症状記録** — 頭痛・歯茎痛・肩の筋肉痛・腰痛・疲労感を0〜10段階評価
- **Google Fit 連携** — 日次歩数を自動取得・反映
- **カレンダー表示** — 痛みの強さを色分け表示
- **グラフ** — 症状ごとの個別グラフを縦並びで一覧
- **編集・削除** — 過去記録の修正・削除
- **悪化要因の管理** — 要因の追加・編集・削除

## データ保存

すべてのデータはブラウザの `localStorage` に保存されます。サーバーへの送信は一切ありません。

---

## Google Fit 連携の設定方法

### 1. Google Cloud Console でプロジェクト作成

1. [Google Cloud Console](https://console.cloud.google.com/) を開く
2. 新しいプロジェクトを作成
3. 「APIとサービス」→「ライブラリ」→ **Fitness API** を有効化

### 2. OAuth 2.0 クライアント ID を取得

1. 「APIとサービス」→「認証情報」→「認証情報を作成」→「OAuth 2.0 クライアント ID」
2. アプリケーションの種類: **ウェブアプリケーション**
3. **承認済みの JavaScript 生成元** にこのアプリのURLを追加  
   例: `https://yourname.github.io`（または `http://localhost:5500` など）
4. 作成されたクライアント ID をコピー（`xxxxxxxx.apps.googleusercontent.com`）

### 3. アプリに設定

1. アプリ右上の「**Fit 連携**」ボタンをタップ
2. コピーしたクライアント ID を貼り付け
3. 「保存して接続」→ Google アカウントで認証
4. 歩数データが自動取得されます

### 同期の仕組み

- アプリ起動時に前回の同期から1時間以上経過していれば自動同期
- グラフタブの「再同期」ボタンで手動同期も可能
- 取得した歩数は `localStorage` にキャッシュ
- 記録フォームで日付を選ぶと、その日の歩数が自動入力（手動で上書き可）

---

## GitHub Pages でのデプロイ

1. このリポジトリを GitHub にプッシュ
2. Settings → Pages → Source を `main` ブランチの `/ (root)` に設定
3. 表示されたURLでアクセス可能（このURLをGoogle Cloud ConsoleのJavaScript生成元に追加）

## 技術スタック

- **HTML / CSS / JavaScript** — フレームワーク不要のシングルファイル
- **[Chart.js](https://www.chartjs.org/)** — グラフ描画（CDN経由）
- **[Google Identity Services](https://developers.google.com/identity)** — OAuth2
- **[Google Fitness REST API](https://developers.google.com/fit/rest)** — 歩数取得
- **localStorage** — データ永続化

## ライセンス

MIT
