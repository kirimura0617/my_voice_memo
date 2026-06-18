# VoxScribe 🎙

音声メモをAIが思考整理し、Obsidianのデイリーノートに追記するWebアプリです。

---

## 概要

話すだけでアイデア・気づき・思考の断片を記録できます。Gemini APIが箇条書きに整理し、確認後にObsidianのデイリーノートへ自動追記します。

```
① 録音 → 話す → 停止
② 文字起こし結果を確認
③ Gemini APIが箇条書きに要約
④ 内容を確認・編集
⑤ Obsidianのデイリーノートに追記
```

---

## 機能

- 🎤 **音声録音** — ブラウザのマイクでリアルタイム文字起こし（Web Speech API）
- ✨ **AI要約** — Gemini APIが思考・アイデアを箇条書きに整理
- 📝 **確認・編集** — 送信前にテキストを自由に編集可能
- 📓 **Obsidian連携** — デイリーノートの末尾に自動追記
- ⚙️ **カスタムテンプレート** — 追記フォーマットを自由に設定可能

---

## 動作環境

| 項目 | 要件 |
|---|---|
| ブラウザ | Google Chrome（推奨）※Web Speech APIのため |
| OS | PC（Windows / macOS / Linux） |
| Obsidian | 起動済みであること |
| プラグイン | [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) |

---

## セットアップ

### 1. Gemini APIキーを取得する

1. [Google AI Studio](https://aistudio.google.com/) にアクセス
2. 「Get API key」からAPIキーを発行（無料枠あり）

### 2. Obsidian Local REST API プラグインを設定する

1. ObsidianのコミュニティプラグインからLocal REST APIをインストール・有効化
2. プラグイン設定画面でAPIキーをコピーしておく
3. Obsidianを起動したままにする

### 3. SSL証明書を許可する（初回のみ）

ブラウザからlocalhost上のObsidianへHTTPS接続するため、初回のみ証明書の許可が必要です。

1. Chromeで `https://127.0.0.1:27124/` を開く
2. 「詳細設定」→「127.0.0.1 にアクセスする（安全ではありません）」をクリック

### 4. アプリを開いて設定する

アプリ右上の設定アイコンから以下を入力して保存します。

| 設定項目 | 内容 |
|---|---|
| Gemini API キー | Google AI Studioで取得したキー |
| Gemini モデル | gemini-2.5-flash（デフォルト推奨） |
| Obsidian API キー | Local REST APIプラグインのキー |
| ホスト | `127.0.0.1`（デフォルト） |
| ポート | `27124`（デフォルト） |

---

## GitHub Pagesへのデプロイ

```bash
# リポジトリをクローン（またはfork）
git clone https://github.com/kirimura0617/voxscribe.git
cd voxscribe

# index.html をルートに置いてpush
git add index.html
git commit -m "Initial commit"
git push origin main
```

GitHubリポジトリの **Settings → Pages → Branch: main / (root)** を選択すると公開されます。

> ⚠️ **APIキーはGitHubにコミットしないでください。** キーの入力はブラウザの設定画面から行い、localStorageに保存されます。

---

## セキュリティについて

- APIキーはすべて**ブラウザのlocalStorageにのみ保存**されます
- サーバーへの送信・第三者への共有は一切行いません
- Gemini APIへの通信はブラウザから直接行われます
- Obsidian Local REST APIへの通信はlocalhost内で完結します

---

## 使い方

1. マイクボタンをクリックして録音開始
2. 話し終わったらもう一度クリックして停止
3. 「AI要約を作成」ボタンをクリック
4. 要約結果を確認・編集
5. 「Obsidianに送る」ボタンで追記完了

---

## カスタムテンプレート

設定画面の「追記テンプレート」で追記フォーマットをカスタマイズできます。

| 変数 | 内容 | 例 |
|---|---|---|
| `{{content}}` | 要約テキスト | - アイデアAについて考えた |
| `{{time}}` | 送信時刻 | 15:30 |
| `{{date}}` | 送信日付 | 2026-06-18 |

**デフォルトテンプレート：**
```
### 🎤 音声メモ ({{time}})
{{content}}
```

---

## 技術構成

| 要素 | 技術 |
|---|---|
| フロントエンド | HTML / CSS / Vanilla JS（単一ファイル） |
| 音声認識 | Web Speech API |
| AI要約 | Gemini API（google generativelanguage） |
| Obsidian連携 | Obsidian Local REST API |
| ホスティング | GitHub Pages |

---

## ライセンス

MIT License
