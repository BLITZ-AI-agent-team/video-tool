# Drive Download セットアップガイド

Google Driveのフォルダを、フォルダ構造そのままローカルにダウンロードできるツールです。
ブラウザDLで起きるzip分割・構造崩壊の問題を解決します。

---

## セットアップ方法

### 事前準備（あなたが手動でやること）

1. 別途共有された `service_account.json` をデスクトップなど分かりやすい場所に保存する
2. Claude Code を開く

### Claude Code に以下を貼り付ける

以下を **そのままコピーして** Claude Code に貼り付けてください。自動でセットアップが始まります:

---

```
Drive Download ツールをセットアップして。以下の手順を全部自動でやって:

1. リポジトリをクローン:
   git clone https://github.com/BLITZ-AI-agent-team/drive-download.git

2. 依存パッケージをインストール:
   pip install google-api-python-client google-auth

3. service_account.json をリポジトリ直下にコピー（デスクトップにあるはず。なければ場所を聞いて）

4. スキルをグローバルに登録:
   mkdir -p ~/.claude/skills/drive-download
   cp drive-download/.claude/skills/drive-download/SKILL.md ~/.claude/skills/drive-download/SKILL.md

5. 全部終わったら「セットアップ完了」と教えて
```

---

セットアップは以上です。完了したら、次から以下のように使えます:

## 使い方

Claude Code でこう話しかけるだけ:

```
このGoogleドライブのフォルダをダウンロードして
https://drive.google.com/drive/u/0/folders/XXXXX
```

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
