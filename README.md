# AITuber Radio Station

AITuber Radio の番組カードをワンクリックで再生できるステーションサイトです。

## 🎧 サイトURL

👉 **https://k3peta.github.io/aituber-radio-station/**

## はじめかた

1. [AITuber Radio](https://github.com/k3peta/aituber-radio) Chrome 拡張機能をインストール
2. [VOICEVOX](https://voicevox.hiroshiba.jp/) または [Style-Bert-VITS2](https://github.com/litagin02/Style-Bert-VITS2) を起動
3. 拡張機能ポップアップの 📋 で ID をコピー → Station のテキストボックスに貼り付けて「接続」
4. 好きな番組カードの ▶ をクリック → 再生開始

**サーバー負荷ゼロ** — 音声合成も AI もすべてローカルで実行。サーバーは静的ファイルを配信するだけ。

## 番組一覧

| カード | テーマ | AI | 時間 |
|---|---|---|---|
| 🌙 怪談ちゃんの夜更かしラジオ | 深夜のゆるい雑談×リスナー交流 | 🤖 必須 | 30分 |
| ☀️ 怪談ちゃんのおはようラジオ | 朝の豆知識バラエティ | 🤖 必須 | 30分 |
| 🌃 真夜中のひとりごと | しっとり哲学系 | 🤖 必須 | 30分 |
| 📚 怪談ちゃんの雑学タイム | 食べ物・動物・宇宙・日本語・人体 | 📝 台本のみ | 15分 |
| 🏯 怪談ちゃんのなるほどヒストリー | 古代〜江戸の歴史エピソード | 📝 台本のみ | 15分 |
| ⛩️ 旅ラジオ 京都編 | 路地裏・グルメ・穴場スポット | 📝 台本のみ | 10分 |
| 🌊 旅ラジオ 沖縄編 | 海・ソーキそば・島文化 | 📝 台本のみ | 10分 |
| ❄️ 旅ラジオ 北海道編 | 大自然・海鮮・温泉 | 📝 台本のみ | 10分 |
| 🎤 VOICEVOX音色カタログ | 30+キャラの声を聴き比べ | 📝 台本のみ | 20分 |
| ☀️ ひるまちラジオ | お便り・雑談・独り言 | 📝 台本のみ | 15分 |

### AI バッジ

| バッジ | 意味 |
|--------|------|
| 🤖 AI必須 | フリートークやコメント返しにLLMが必要 |
| 📝 台本のみ | AIなしで完全再生可能 |

## 台本の書き方

> 詳細仕様は [SETLIST_FORMAT.md](SETLIST_FORMAT.md) を参照

## カードの作り方

`cards/` に新しいフォルダを作って、`card.json` と `setlist.md` を置くだけ。

```json
{
  "id": "my-show",
  "title": "私のラジオ番組",
  "author": "your-name",
  "description": "番組の説明",
  "duration": "30min",
  "ai": "none",
  "tags": ["雑談"],
  "setlist": "setlist.md",
  "media": {
    "media/bgm.mp3": "assets/bgm.mp3"
  },
  "credits": [
    { "file": "bgm.mp3", "title": "曲名", "artist": "アーティスト名", "source": "YouTube Audio Library" }
  ]
}
```

### `ai` フィールド

| 値 | 意味 |
|----|------|
| `none` | AI不要（全台本）|
| `optional` | AIがあるとより楽しい |
| `required` | AI必須 |

## TTS エンジン

拡張機能側の「🔊 TTS エンジン設定」で切り替え可能。

| エンジン | ポート |
|---------|--------|
| VOICEVOX | 50021 |
| Style-Bert-VITS2 | 5000 |
| COEIROINK | 50032 |
| AivisSpeech | 10101 |

## 🔒 セキュリティ

| 項目 | 詳細 |
|---|---|
| **通信方向** | Station → 拡張機能（一方向） |
| **送信内容** | カード JSON のみ（台本テキスト + メディア URL） |
| **メディア取得** | 拡張機能が GitHub Pages 上の静的ファイルを fetch |
| **実行される処理** | テキスト読み上げ（TTS）+ 音声/画像再生のみ |
| **ローカルデータ** | API キー等は `chrome.storage.local` にのみ保存 |
| **許可サイト** | `externally_connectable` で接続元を制限 |

## Music Credits

| 用途 | 曲名 | アーティスト |
|---|---|---|
| OP/ED ジングル | O Chanukah (Instrumental) | Jingle Punks |
| コーナージングル | Jingle Bells | The Soundlings |
| BGM | Et Voila | Chris Haugen |

すべて YouTube Audio Library のフリー素材です。

## ライセンス

MIT License
