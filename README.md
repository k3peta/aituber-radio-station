# AITuber Radio Station

AITuber Radio の台本カードをワンクリックで再生できるステーションサイトです。

## 🎧 サイトURL

👉 **https://k3peta.github.io/aituber-radio-station/**

## 仕組み

1. [AITuber Radio](https://github.com/k3peta/aituber-radio) Chrome 拡張機能をインストール
2. [VOICEVOX](https://voicevox.hiroshiba.jp/) を起動
3. Station サイトで好きなカードの「▶ 再生」をクリック
4. 拡張機能が台本とメディアを取得 → ローカルで VRM キャラクターが喋り出す

**サーバー負荷ゼロ** — 音声合成も AI もすべてローカルで実行。サーバーは静的ファイルを配信するだけ。

## カード一覧

| カード | テーマ | 時間 |
|---|---|---|
| 怪談ちゃんの夜更かしラジオ | 深夜のゆるい雑談 | 30分 |
| 怪談ちゃんのおはようラジオ | 朝の豆知識バラエティ | 30分 |
| 真夜中のひとりごと | しっとり哲学系 | 30分 |

## カードの作り方

`cards/` に新しいフォルダを作って、`card.json` と `setlist.md` を置くだけ。

```json
{
  "id": "my-show",
  "title": "私のラジオ番組",
  "author": "your-name",
  "description": "番組の説明",
  "duration": "30min",
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

## 🔒 セキュリティ

Station サイトと拡張機能の連携は以下のように設計されています。

| 項目 | 詳細 |
|---|---|
| **通信方向** | Station → 拡張機能（一方向）。拡張機能からの送信はなし |
| **送信内容** | カード JSON のみ（台本テキスト + メディア URL） |
| **メディア取得** | 拡張機能が GitHub Pages 上の静的ファイルを fetch するだけ |
| **実行される処理** | テキスト読み上げ（VOICEVOX）+ 音声/画像再生のみ |
| **外部送信** | ユーザーが LLM API を設定している場合のみ、AI フリートーク用に使用 |
| **ローカルデータ** | API キーなどのユーザー設定は `chrome.storage.local` にのみ保存 |
| **許可サイト** | `manifest.json` の `externally_connectable` で接続元を制限 |

カードに含まれるのは **テキスト（台本）と静的ファイルの URL** だけです。スクリプトの実行や任意コードの注入は行いません。

## Music Credits

サンプルカードで使用している楽曲はすべて YouTube Audio Library のフリー素材です。

| 用途 | 曲名 | アーティスト |
|---|---|---|
| OP/ED ジングル | O Chanukah (Instrumental) | Jingle Punks |
| コーナージングル | Jingle Bells | The Soundlings |
| BGM | Et Voila | Chris Haugen |

## ライセンス

MIT License
