---
description: AITuber Radio Stationにカードを追加・更新する手順
---

# カード追加・更新ワークフロー

AITuber Radio Station (`aituber-radio-station`) にカードを追加・更新する際の手順。
ミスが起きやすいポイント（index.json の更新忘れ、CARD_CATEGORIESへの登録漏れ）を防ぐためにスキル化。

## 前提
- リポジトリ: `/Users/ys/aituber-radio-station`
- カードディレクトリ: `cards/{card_id}/`
- 各カードには `card.json` と `setlist.md` が必要

## 手順

### 1. カードファイルを作成
// turbo

```
cards/{card_id}/card.json   # カード設定（id, title, description, speakers, tags等）
cards/{card_id}/setlist.md  # 台本（YAMLフロントマター + マークダウン形式）
cards/{card_id}/media/      # （任意）BGMやSE、画像ファイル
```

**card.json の必須フィールド:**
```json
{
  "id": "card_id",
  "title": "タイトル",
  "author": "k3peta",
  "description": "説明文",
  "duration": "10min",
  "ai": "none",
  "tags": ["タグ1", "タグ2"],
  "setlist": "setlist.md"
}
```

**⚠️ `setlist` フィールドを忘れると再生に失敗する！**

### 2. cards/index.json を再生成
// turbo

以下のPythonスクリプトを実行して `cards/index.json` を自動再生成する。
**手動でindex.jsonを編集しない**こと。必ずスクリプトで生成する。

```bash
cd /Users/ys/aituber-radio-station && python3 -c "
import json, os
cards_dir = 'cards'
index = []
for name in sorted(os.listdir(cards_dir)):
    card_path = os.path.join(cards_dir, name, 'card.json')
    if os.path.isfile(card_path):
        with open(card_path) as f:
            card = json.load(f)
        card['id'] = name
        index.append(card)
with open(os.path.join(cards_dir, 'index.json'), 'w') as f:
    json.dump(index, f, ensure_ascii=False, indent=2)
print(f'{len(index)} cards indexed')
for c in index:
    print(f'  {c[\"id\"]}: {c.get(\"title\",\"?\")}')
"
```

**確認ポイント:** 新規カードのIDが出力に含まれていること。

### 3. index.html の CARD_CATEGORIES にIDを追加

`index.html` の `CARD_CATEGORIES` オブジェクトに、新規カードのIDを適切なカテゴリに追加する。

| カテゴリ | 内容 |
|---------|------|
| `radio` | ラジオ番組（ニュース、雑談、旅、雑学） |
| `learn` | 学習番組（Python、SQL、Git等） |
| `guide` | ガイド・デモ・カタログ（howto、音声カタログ、ジェスチャーデモ等） |
| `other` | その他（ASMR等） |

**これを忘れるとステーションページに表示されない！**

### 4. index.html の FALLBACK_CARDS にフォールバックデータを追加（推奨）

`file://` プロトコルでアクセスした場合に `fetch` が失敗するため、
`FALLBACK_CARDS` オブジェクトにもカードデータを追加しておくとローカルでも動作する。

### 5. Gitコミット & プッシュ
// turbo

```bash
cd /Users/ys/aituber-radio-station && git add -A && git status
```

コミットメッセージ例:
```bash
git commit -m "feat: 新カード追加 (card_id)"
git push origin main
```

### 6. 検証

- GitHub Pagesで新カードが表示されることを確認
- 拡張機能から再生できることを確認
- `#card-{id}` のページ内リンクでスクロールされることを確認

## チェックリスト（コミット前に確認）

- [ ] `cards/{id}/card.json` が存在する
- [ ] `cards/{id}/setlist.md` が存在する
- [ ] `cards/index.json` をPythonスクリプトで再生成した
- [ ] `index.html` の `CARD_CATEGORIES` に新IDを追加した
- [ ] `index.html` の `FALLBACK_CARDS` にデータを追加した（推奨）
- [ ] メディアファイルがある場合は `cards/{id}/media/` に配置した
