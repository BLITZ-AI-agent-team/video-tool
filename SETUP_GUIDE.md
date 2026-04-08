# Drive Download セットアップガイド

Google Driveのフォルダを、フォルダ構造そのままローカルにダウンロードできるツールです。
ブラウザDLで起きるzip分割・構造崩壊の問題を解決します。

---

## セットアップ（5分で完了）

### Step 1: リポジトリをクローン

```bash
git clone https://github.com/BLITZ-AI-agent-team/drive-download.git
cd drive-download
```

### Step 2: 依存パッケージをインストール

```bash
pip install google-api-python-client google-auth
```

### Step 3: サービスアカウントキーを配置

別途共有された `service_account.json` を `drive-download/` フォルダの直下に置いてください。

```
drive-download/
  service_account.json  ← ここに置く
  src/
  README.md
  ...
```

### Step 4: Claude Code にスキルを登録

リポジトリ内にスキルファイルが含まれています。
Claude Code でこのツールを使うには、**スキルをコピー**します:

```bash
# スキル用フォルダを作成（既にあればスキップ）
mkdir -p ~/.claude/skills/drive-download

# スキルファイルをコピー
cp drive-download/.claude/skills/drive-download/SKILL.md ~/.claude/skills/drive-download/SKILL.md
```

> **~/.claude/** は Claude Code のグローバル設定フォルダです。
> ここにスキルを置くと、どのプロジェクトからでもスキルが使えるようになります。

---

## 使い方

### Claude Code から（スキル登録後）

Claude Code を開いて、こう話しかけるだけ:

```
「このGoogleドライブのフォルダをダウンロードして」
https://drive.google.com/drive/u/0/folders/XXXXX
```

### コマンドラインから

```bash
cd drive-download
python -m src.module7.main "https://drive.google.com/drive/u/0/folders/XXXXX"
```

保存先を指定したい場合:
```bash
python -m src.module7.main "URL" -d /好きなフォルダ
```

---

## 初回ダウンロード時の注意

ダウンロードしたいフォルダ/ファイルを、サービスアカウントに共有する必要があります:

1. Google Drive でダウンロードしたいフォルダを開く
2. 右クリック → **共有**
3. 以下のメールアドレスを追加（**閲覧者**でOK）:

```
aiagent-dev@aiagent-dev-489706.iam.gserviceaccount.com
```

一度共有すれば、そのフォルダ内のファイルは何度でもダウンロードできます。

---

## よくある質問

**Q: 同じフォルダを2回ダウンロードしたらどうなる？**
差分チェックが働き、変更のないファイルはスキップされます。更新されたファイルだけ再ダウンロードします。

**Q: 「File not found」エラーが出た**
対象フォルダがサービスアカウントに共有されていません。上の「初回ダウンロード時の注意」を確認してください。

**Q: Google スプレッドシートやドキュメントはどうなる？**
自動的に変換されます: Docs→PDF、Sheets→xlsx、Slides→pptx
