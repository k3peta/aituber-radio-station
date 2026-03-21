# AITuber Radio Station — カード仕様書

## ディレクトリ構成

```
aituber-radio-station/
├── index.html              # ステーショントップページ
├── assets/                 # 📦 共有メディアファイル（全カード共通）
│   ├── bgm.mp3             # BGM
│   ├── bgm_chill.mp3       # BGM（ジムノペディ）
│   ├── jingle1.mp3         # ジングル1
│   ├── jingle2.mp3         # ジングル2
│   ├── opening.jpg         # オープニング画像
│   ├── ending.jpg          # エンディング画像
│   ├── slide_select.png    # SQL用フロート画像
│   └── slide_basics.png    # Python用フロート画像
└── cards/
    └── {card_id}/
        ├── card.json       # カードメタデータ
        └── setlist.md      # 台本
```

> [!IMPORTANT]
> メディアファイルは必ず **ルートの `assets/`** に配置する。
> `cards/{id}/assets/` にローカル配置しない。
> ステーションの URL解決は `STATION_BASE/{remotePath}` で行われるため、
> `remotePath` が `assets/bgm.mp3` の場合、`https://...station/assets/bgm.mp3` となる。

## card.json フォーマット

```json
{
  "id": "card_id",
  "title": "番組タイトル",
  "author": "k3peta",
  "description": "番組の説明文",
  "duration": "10min",
  "ai": "none",
  "tags": ["タグ1", "タグ2"],
  "series": "シリーズ名（任意）",
  "episode": 1,
  "setlist": "setlist.md",
  "media": {
    "media/bgm.mp3": "assets/bgm.mp3",
    "media/slide_xxx.png": "assets/slide_xxx.png"
  },
  "credits": [
    { "file": "bgm.mp3", "title": "曲名", "artist": "アーティスト", "source": "出典" }
  ]
}
```

### フィールド説明

| フィールド | 型 | 必須 | 説明 |
|-----------|------|------|------|
| `id` | string | ✅ | カードID（ディレクトリ名と一致） |
| `title` | string | ✅ | 番組タイトル |
| `author` | string | ✅ | 作者 |
| `description` | string | ✅ | 番組の説明 |
| `duration` | string | ✅ | 所要時間（例: `"10min"`） |
| `ai` | string | ✅ | AI使用: `"none"` / `"optional"` / `"required"` |
| `tags` | string[] | ✅ | タグ一覧 |
| `series` | string | ❌ | シリーズ名 |
| `episode` | number | ❌ | エピソード番号 |
| `setlist` | string | ✅ | 台本ファイル名（通常 `"setlist.md"`） |
| `media` | object | ✅ | メディアマッピング（下記参照） |
| `credits` | object[] | ✅ | クレジット情報 |

### media マッピング

```
キー:   台本内で参照する名前   例: "media/bgm.mp3"
値:     ステーション上のパス     例: "assets/bgm.mp3"
```

> [!WARNING]
> 値は **ルート `assets/` からの相対パス** を指定する。
> `cards/{id}/assets/xxx` のような個別パスは使わない。

## setlist.md フォーマット

### YAMLフロントマター

```yaml
---
title: 番組タイトル
speaker: 38          # VOICEVOX話者ID
speed: 0.95          # 話速
pause_between: 800   # セリフ間の間隔(ms)
---
```

### セグメント構文

```markdown
# セグメントタイトル
[type: talk]
[bgm: media/bgm.mp3]    # BGM開始
[volume: 0.2]            # BGM音量
[float: media/xxx.png]   # フロート画像表示

セリフテキスト

# 次のセグメント
[type: talk]
[float: none]            # フロート画像を消す
[bgm: none]              # BGM停止

セリフテキスト
```

### タグ一覧

| タグ | 説明 | 例 |
|------|------|-----|
| `[type: talk]` | トークセグメント | `[type: talk]` |
| `[bgm: path]` | BGM開始 | `[bgm: media/bgm.mp3]` |
| `[bgm: none]` | BGM停止 | `[bgm: none]` |
| `[volume: n]` | BGM音量 | `[volume: 0.2]` |
| `[float: path]` | フロート画像表示 | `[float: media/slide.png]` |
| `[float: none]` | フロート画像非表示 | `[float: none]` |
| `[bg: path]` | 背景画像変更 | `[bg: media/bg.jpg]` |

### {読み} 構文

表示テキストとTTS読み上げテキストを分けたい場合：

```
SELECT * FROM users; {セレクト、アスタリスク、フロム、ユーザーズ。}
```

- 表示: `SELECT * FROM users;`
- TTS: `セレクト、アスタリスク、フロム、ユーザーズ。`

## index.html の CARD_IDS

新しいカードを追加した場合、`index.html` 内の `CARD_IDS` 配列にIDを追加する必要がある：

```javascript
const CARD_IDS = ['news_morning', ..., 'python_ep01', 'python_ep02', 'sql_ep01', 'sql_ep02']
```

## 新規カード追加チェックリスト

1. [ ] `cards/{id}/card.json` を作成
2. [ ] `cards/{id}/setlist.md` を作成
3. [ ] メディアファイルを **ルート `assets/`** に配置
4. [ ] `card.json` の `media` マッピングが `assets/xxx` を指してることを確認
5. [ ] `index.html` の `CARD_IDS` にIDを追加
6. [ ] `git push` してGitHub Pagesにデプロイ
