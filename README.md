# 企業ルール準拠PPT作成Skill｜Usausa Corporate Rule PPT

企業のブランドガイドラインやPowerPointテンプレートに準拠した資料作成を支援する、Claude Skills向けの業務改善ツールです。

企業ルールをYAMLで一元管理し、スライドの生成・体裁統一・ルールチェックを体系化することで、資料作成の属人化を抑え、品質の安定化を目指します。

> **設計コンセプト：ルールを1か所に定義し、すべてのスライドに一貫して適用する。**

---

## 📌 Overview

PowerPoint資料の作成・修正では、企業ごとの配色、フォント、余白、ロゴ、フッターなどのルールを確認し、各スライドに反映する必要があります。

本Skillでは、企業ルールとスライドコンテンツを分離し、再利用可能な資料作成フローを設計します。

### 解決したい課題

- 資料ごとにフォント・配色・余白が異なる
- ブランドガイドラインへの準拠確認に時間がかかる
- 複数のPowerPoint資料を統一する作業が煩雑
- 修正時にレイアウトや書式の不整合が発生する
- 担当者の経験や判断に依存している

## ✨ Features

| 機能 | 内容 |
|---|---|
| 企業ルール管理 | YAMLで色・フォント・余白・ロゴ・フッターなどを定義 |
| テンプレート解析 | PowerPointからルール候補を抽出 |
| スライド構成設計 | 章立て・タイトル・メッセージを整理 |
| PowerPoint生成 | 共通テーマとレイアウトに基づく資料生成 |
| ルールチェック | 定義されたルールへの準拠を検査 |
| 品質保証 | ファイル検証・PDF変換・画像による目視確認 |
| 検査結果の報告 | 出典・仮置き・要確認項目・警告を明示 |

※ 各機能は設計上の機能一覧です。利用には対応するスクリプトの実装と動作検証が必要です。

## 🏗️ Architecture

```text
Corporate Template / Brand Guidelines
                  │
                  ▼
         Rule Extraction
                  │
                  ▼
            rules.yaml
       企業ルール・書式規則
                  │
                  ├──────────────┐
                  │              │
                  ▼              ▼
           User Review     content.yaml
                           スライド内容
                  │              │
                  └──────┬───────┘
                         ▼
                  PowerPoint Build
                         │
                         ▼
                      out.pptx
                         │
                         ▼
                  Lint & Validation
                         │
                         ▼
                  PDF / Visual QA
                         │
                         ▼
                 Quality Report
```

### 設計方針

**1. ルールとコンテンツを分離する**

デザイン規則とスライドの内容を別ファイルで管理し、修正や再利用を容易にします。

**2. 企業の公式情報を優先する**

ブランドガイドラインや公式テンプレートを根拠とし、不明なルールを推測で補完しません。

**3. 生成前に合意する**

企業ルールとスライド構成を事前に確認し、完成後の手戻りを抑えます。

**4. 自動検査と目視確認を組み合わせる**

機械的なルールチェックに加え、文字のはみ出し、可読性、レイアウトの統一感を確認します。

## 🛠️ Tech Stack

| 技術 | 用途 |
|---|---|
| Claude Skills | 作業手順・判断基準の体系化 |
| YAML | 企業ルール・スライド内容の定義 |
| Python | テンプレート解析・ルール検査 |
| Node.js | PowerPoint生成処理 |
| PptxGenJS | PowerPointファイルの生成 |
| LibreOffice | PDF変換・表示確認 |
| Git / GitHub | ソース管理・変更履歴管理 |

## 📂 Directory Structure

```text
usausa-corporate-rule-ppt/
├── SKILL.md
├── README.md
├── assets/
│   ├── corporate-rules.template.yaml
│   └── content.sample.yaml
├── scripts/
│   ├── extract_rules.py
│   ├── build_deck.js
│   └── lint_deck.py
└── references/
    └── qa-checklist.md
```

| ファイル | 役割 |
|---|---|
| `SKILL.md` | Skillの目的・処理手順・判断基準 |
| `corporate-rules.template.yaml` | 企業ルールの定義テンプレート |
| `content.sample.yaml` | スライド内容のサンプル |
| `extract_rules.py` | PowerPointテンプレートの設定抽出 |
| `build_deck.js` | PowerPoint生成 |
| `lint_deck.py` | ルール準拠の検査 |
| `qa-checklist.md` | 最終品質確認 |

## 🚀 Getting Started

### 1. リポジトリを取得する

```bash
git clone <YOUR_REPOSITORY_URL>
cd usausa-corporate-rule-ppt
```

`<YOUR_REPOSITORY_URL>` は、作成したGitHubリポジトリのURLに置き換えてください。

### 2. 企業ルールを準備する

公式テンプレートやガイドラインを確認し、企業ルールのYAMLを作成します。

```text
assets/corporate-rules.template.yaml
                  ↓
              rules.yaml
```

色・フォント・レイアウト・ロゴ・フッターなどを定義します。

不明な項目は「要確認」として残し、ユーザーに確認します。

### 3. スライド内容を定義する

`assets/content.sample.yaml` を参考に、タイトル、本文、比較情報などを定義します。

### 4. PowerPointを生成する

以下は、生成スクリプトを実装した環境での実行例です。

```bash
node scripts/build_deck.js \
  rules.yaml \
  content.yaml \
  out.pptx \
  --strict
```

`--strict` は、実装側でルール違反時の停止処理を用意した場合に機能します。

### 5. ルールを検査する

```bash
python3 scripts/lint_deck.py rules.yaml out.pptx
```

その後、PowerPointファイルの構造検証、PDF変換、全スライドの画像確認を実施します。

※ 本リポジトリの各スクリプト、依存関係、実行コマンドは、実装状況に応じて整備してください。

## 🎨 Supported Layouts

以下のレイアウトを基本形として設計しています。

| Layout | 用途 |
|---|---|
| `cover` | 表紙 |
| `section` | 章の区切り |
| `title_bullets` | タイトル＋箇条書き |
| `two_column` | 比較・2列構成 |
| `kpi` | 数値・指標の提示 |
| `closing` | まとめ・締めくくり |

1スライド1メッセージを基本とし、情報を詰め込みすぎず、読み手が要点を把握しやすい構成を目指します。

## ✅ Quality Assurance

資料を提示する前に、次の項目を確認します。

- [ ] 企業ルールの出典を確認した
- [ ] 不明なルールを推測で補完していない
- [ ] タイトル・フォント・配色・余白が統一されている
- [ ] 許可されたレイアウトを使用している
- [ ] 文字や図表がスライドからはみ出していない
- [ ] 数値や事例に出典がある
- [ ] PowerPointファイルの構造を検証した
- [ ] PDF化して全スライドを確認した
- [ ] 残っている警告や要確認事項を明示した

## 🔒 Security & Privacy

企業資料を取り扱う場合は、次の点に注意します。

- 機密情報や個人情報を必要以上に外部サービスへ送信しない
- 社内規定に従ってAIサービスの利用可否を確認する
- ロゴやテンプレートの利用条件を確認する
- APIキーや認証情報をGitHubへコミットしない
- 公開リポジトリには、公開許可のあるサンプル資料のみを掲載する

## 🗺️ Roadmap

- [ ] 企業ルールYAMLの標準スキーマ整備
- [ ] PowerPointテンプレート解析の実装
- [ ] 共通テーマ・レイアウトによる生成処理
- [ ] ルール違反の自動検査
- [ ] PDF・画像による品質確認の自動化
- [ ] 検査レポートの生成
- [ ] 複数デッキの一括検査
- [ ] ルール変更履歴の管理

## 💡 Portfolio Value

本プロジェクトでは、AI活用だけでなく、業務ルールの構造化、設定管理、自動生成、品質保証までを一連の仕組みとして設計します。

特に、次の観点をポートフォリオとして示すことを目指します。

- **AI活用：** Claude Skillsによる作業手順の標準化
- **設計力：** YAMLによるルールとコンテンツの分離
- **開発力：** Python・JavaScriptによる処理の自動化
- **品質保証：** lint・検証・目視確認の組み合わせ
- **DX支援：** 資料作成の属人化を抑える業務設計

## 📄 License

個人利用に限り無料。

---

**Usausa Corporate Rule PPT**  
企業ルールを仕組みに変え、資料作成をもっと統一的に、もっと効率的に。
