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
  }
}
```

## ライセンス

MIT License
