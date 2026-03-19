# セットリスト台本フォーマット仕様

AITuber Radio のセットリスト（`.md`）ファイルの書き方です。

## 基本構造

```
---
YAML フロントマター
---

# セグメント名
[type: セグメントタイプ]
[プロパティ: 値]
テキスト行（talk/script の場合）
```

---

## フロントマター（必須）

```yaml
---
title: 番組タイトル
speaker: 38              # VOICEVOX スピーカーID（38=怪談ぺたん）
speed: 0.90              # 読み上げ速度（0.5〜2.0）
loop: false              # 番組をループ再生するか
pause_between: 1500      # セグメント間のポーズ（ミリ秒）
---
```

### 主なスピーカーID

| ID | キャラクター |
|----|------------|
| 3  | ずんだもん |
| 38 | 怪談ぺたん |
| 46 | No.7 |
| 8  | 春日部つむぎ |

> 完全なリストは VOICEVOX エンジンの `/speakers` で確認できます。

---

## セグメント

各セグメントは `# セグメント名` で始まります。

```
# オープニングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.7]
こんばんは！今日も楽しくやっていくよ！
```

> ⚠️ `## ` や `### ` ではなく、必ず `# `（h1）を使ってください。

---

## セグメントタイプ

### `talk` — 台本トーク（AI不要）

事前に書かれたセリフを読み上げます。

```
# オープニングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.7]
こんばんは！怪談ちゃんだよ。
今日もまったり雑談していくっすよ。
```

| プロパティ | 値 | 説明 |
|-----------|-----|------|
| `speaker` | スピーカーID | このセグメントだけ声を変更（フロントマターのデフォルトを上書き） |
| `emotion` | `neutral` `happy` `sad` `surprised` `relaxed` | 感情（VOICEVOX スタイル） |
| `intensity` | `0.0`〜`1.0` | 感情の強さ |
| `bgm` | ファイルパス | BGM を開始（ループ再生） |
| `bgmvolume` | `0.0`〜`1.0` | BGM 音量（デフォルト: 0.25） |
| `bgmstop` | `true` | BGM を停止 |
| `overlay` | ファイルパス | 画面に画像を表示 |

### `jingle` — ジングル・SE（AI不要）

音声ファイルを再生します。オプションで再生中にセリフを重ねられます。

```
# オープニングジングル
[type: jingle]
[file: media/jingle1.mp3]
[overlay: media/opening.jpg]
[duration: 12]
[fadeOut: 3]
[speakAt: 3]
[speakText: 怪談ちゃんの番組、始まるよ〜！]
```

| プロパティ | 値 | 説明 |
|-----------|-----|------|
| `file` | ファイルパス | 再生する音声ファイル |
| `duration` | 秒数 | 再生時間（これを過ぎるとフェードアウト） |
| `fadeOut` | 秒数 | フェードアウト時間 |
| `speakAt` | 秒数 | ジングル開始から何秒後にセリフを話すか |
| `speakText` | テキスト | ジングル中に話すセリフ |
| `overlay` | ファイルパス | ジングル中に表示する画像 |

### `freetalk` — AIフリートーク（AI必要）

LLM を使ってキャラクターが自由にトークします。

```
# フリートーク: 食べ物の話
[type: freetalk]
[bgm: media/bgm_chill.mp3]
[topic: 最近ハマっている食べ物]
[hook: コンビニで見つけた新商品がめちゃくちゃ美味しかった話]
```

| プロパティ | 値 | 説明 |
|-----------|-----|------|
| `topic` | テキスト | トークのテーマ |
| `hook` | テキスト | 話の導入（LLM へのヒント） |

### `comments` — コメント読み上げ（AI必要）

YouTube ライブチャットのコメントを拾って反応します。

```
# お便りコーナー
[type: comments]
[bgm: media/bgm_chill.mp3]
```

### `script` — 朗読（AI不要）

怪談や物語などの長文テキストを朗読します。

```
# 怪談「夜の学校」
[type: script]
[bgm: media/bgm_horror.mp3]
[reading: readings/yoru_no_gakkou.txt]
```

| プロパティ | 値 | 説明 |
|-----------|-----|------|
| `reading` | ファイルパス | 朗読するテキストファイル |

### `reaction` — 朗読後の感想（AI必要）

直前の朗読に対して AI が感想を語ります。

```
# 感想トーク
[type: reaction]
[bgm: media/bgm_chill.mp3]
```

---

## メディアパス

セットリスト内のメディアパスは `media/` で始めます。

```
[file: media/jingle1.mp3]
[bgm: media/bgm_chill.mp3]
[overlay: media/opening.jpg]
```

Station サイトから再生する場合、`card.json` の `media` マッピングに従って自動的に URL に変換されます。

---

## コメント

HTML コメントが使えます。VOICEVOX には読まれません。

```
<!-- このセグメントは約3分 -->
```

---

## 30分番組のテンプレート（AI不要）

```
---
title: 番組タイトル
speaker: 38
speed: 0.90
loop: false
pause_between: 1500
---

# オープニングジングル
[type: jingle]
[file: media/jingle1.mp3]
[overlay: media/opening.jpg]
[duration: 12]
[fadeOut: 3]
[speakAt: 3]
[speakText: 番組名、はじまるよ〜！]

# オープニングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.7]
こんばんは！（挨拶と今日のテーマ紹介）

# コーナージングル
[type: jingle]
[file: media/jingle2.mp3]
[duration: 8]
[fadeOut: 2]
[speakAt: 2]
[speakText: コーナー名！]

# コーナー1
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: neutral]
[intensity: 0.7]
（本編トーク。1セグメント = 3〜8行程度が目安）

# つなぎ
[type: talk]
[emotion: happy]
[intensity: 0.7]
（コーナー間のつなぎトーク。1〜3行）

<!-- 以下コーナーを繰り返し -->

# エンディングトーク
[type: talk]
[bgm: media/bgm_chill.mp3]
[emotion: happy]
[intensity: 0.7]
（締めの挨拶）

# エンディングジングル
[type: jingle]
[file: media/jingle1.mp3]
[overlay: media/ending.jpg]
[duration: 15]
[fadeOut: 3]
[speakAt: 3]
[speakText: また次回！おやすみ〜！]
```

### 時間の目安

- VOICEVOX の読み上げ速度 0.90 で、**1行（40〜60文字）≒ 5〜8秒**
- ジングル: 8〜15秒
- 30分番組: 約200〜250行のセリフ + ジングル5〜7箇所

---

## card.json のフォーマット

Station サイトに登録するためのメタデータです。

```json
{
  "id": "カードID（フォルダ名と一致）",
  "title": "番組タイトル",
  "author": "作者名",
  "description": "番組の説明（1〜2文）",
  "duration": "30min",
  "ai": "none | optional | required",
  "tags": ["タグ1", "タグ2"],
  "setlist": "setlist.md",
  "media": {
    "media/jingle1.mp3": "assets/jingle1.mp3",
    "media/jingle2.mp3": "assets/jingle2.mp3",
    "media/bgm_chill.mp3": "assets/bgm_chill.mp3",
    "media/opening.jpg": "assets/opening.jpg",
    "media/ending.jpg": "assets/ending.jpg"
  },
  "credits": [
    { "file": "jingle1.mp3", "title": "曲名", "artist": "アーティスト名", "source": "YouTube Audio Library" }
  ]
}
```

### `ai` フィールド

| 値 | 意味 | 使えるセグメント |
|----|------|----------------|
| `none` | AI不要（全台本） | `talk`, `jingle`, `script` のみ |
| `optional` | AIがあるとより楽しい | 上記 + `freetalk` 等があるが無くても動く |
| `required` | AI必須 | `freetalk`, `comments`, `reaction` を含む |
