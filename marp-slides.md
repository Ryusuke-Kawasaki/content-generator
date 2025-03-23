---
marp: true
theme: default
paginate: true
backgroundColor: #fff
---

# GraphAIを活用した<br>マルチプラットフォームコンテンツジェネレーター

---

## 1. プロジェクト概要

- **名前**: GraphAIを活用したマルチプラットフォームコンテンツジェネレーター
- **目的**: 一つのテーマから複数プラットフォーム向けの最適化コンテンツを自動生成
- **対応プラットフォーム**: 
  - YouTube
  - Twitter
  - ブログ

---

## 2. アーキテクチャと実装

![bg right:40% 80%](https://via.placeholder.com/500x600)

**入力**: ユーザーからのテーマ

**処理フロー**:
1. テーマ入力 → プラットフォームごとに処理
2. プラットフォーム特性に合わせたプロンプト生成
3. GPT-4oによるコンテンツ生成
4. 生成コンテンツの取得

---

## プラットフォーム定義

各プラットフォームごとの形式・文字数制限を静的に定義

```javascript
{
  "youtube": {
    "format": "動画スクリプト",
    "maxLength": 2000
  },
  "twitter": {
    "format": "ツイート",
    "maxLength": 140
  },
  "blog": {
    "format": "ブログ記事",
    "maxLength": 5000
  }
}
```

---

## 3. デモンストレーション

### 入力例
```
テーマ: AIと教育の未来
```

### 出力例
- **YouTube**: 教育AI革命について解説する5分動画スクリプト
- **Twitter**: AI教育ツールについての簡潔なツイート
- **ブログ**: AIが教育に与える影響についての詳細な記事

---

## 4. 技術的知見の共有

### デバッグのポイント
```yaml
SampleNode:
  console:
    before: "SampleNode開始"
    after: true
```

- `console.before`/`console.after`を活用した処理状況の可視化

---

### コールバックメソッドの利用
```js
    const graphai = new GraphAI(graph_data, agents, { agentFilters });
    graphai.registerCallback((callbackParam) => {
      console.log(`result: ${JSON.stringify(callbackParam)}`);
    });
```

- Node環境上で実行して詳細な状態を把握

---

### yamlからjsonへの変換
```
graphai --json sample.yaml
```

- Node環境上で実行したい場合、yamlをjsonに変換する必要があるときに

---

## ネストグラフの制約と回避策

### 制約
- 静的ノード内で他のノードの値を展開できない
  - 配列データをネストグラフでシーケンシャルにループすることができない
### 回避策
- ネストグラフをつかったループはしない。Mapによる並列処理で代用。
- シーケンシャルに実行したい場合は...

---

# まとめ

- **効率性**: 短時間で複数プラットフォーム向けのコンテンツを自動生成
- **柔軟性**: GraphAIのフロー制御により複雑な処理を実現
- **拡張性**: 新しいプラットフォームも容易に追加可能
