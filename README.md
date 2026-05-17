# hsp-script

HSP3/OpenHSP のスクリプトを書く・直す・レビューする・説明するための skill です。Codex および Claude Code に対応しています。

## 対応範囲

- 通常の HSP3 ウィンドウ付きスクリプト
- HSPCL 向けのコンソールスクリプト
- HSP3Dish 向けスクリプト
- HGIMG4 向けスクリプト
- `.as` モジュールファイル
- OpenHSP リポジトリ内の sample、help、test 用コード

このskillは、Codex や Claude Code が HSP らしい書き方を保てるように、ラベル、`repeat`/`loop`、`gosub`、コマンド形式の文、HSPプリプロセッサ、Windows版HSPパッケージの構成、OpenHSPリポジトリ内の慣例を参照するための指示をまとめています。

主な想定環境は、利用者が多いと思われるWindows版HSP 3.7パッケージです。`hsed3.exe`、`hspcmp.exe`、`hsp3.exe`、`hsp3cl.exe`、`hsp3dish.exe`、`common/`、`sample/`、`doclib/`、`hsphelp/` を通常の参照先として扱います。Linux+OpenHSPのソースツリーは、開発・検証向けの補足環境として扱います。

## インストール

### Codex

このリポジトリを任意の作業ディレクトリに clone し、リポジトリ内の `skills/` ディレクトリを Codex の skills ディレクトリへシンボリックリンクします。

```bash
git clone https://github.com/<user>/hsp-script-skill.git ~/git/hsp-script-skill
mkdir -p ~/.codex/skills
ln -s ~/git/hsp-script-skill/skills ~/.codex/skills/hsp-skills
```

すでに `~/.codex/skills/hsp-skills` に直接 clone したディレクトリがある場合は、退避または削除してからリンクを作成してください。

環境によっては、Codex の再起動または skill の再読み込みが必要です。

### Claude Code

このリポジトリを任意の作業ディレクトリに clone し、`skills/` ディレクトリを Claude Code の personal skills ディレクトリへシンボリックリンクします。

```bash
git clone https://github.com/<user>/hsp-script-skill.git ~/git/hsp-script-skill
mkdir -p ~/.claude/skills
ln -s ~/git/hsp-script-skill/skills ~/.claude/skills/hsp-script
```

`~/.claude/skills/hsp-script/SKILL.md` として認識され、すべてのプロジェクトで有効になります。プロジェクト単位で使う場合は、`~/.claude/skills/` の代わりにプロジェクトルートの `.claude/skills/` にリンクしてください。

`SKILL.md` の変更はセッション中にライブで反映されます（再起動不要）。新規作成した場合のみ Claude Code の再起動が必要です。

## 使い方

プロンプト内で HSP、HSP3、OpenHSP、`.hsp`、`.as` などに触れると、このskillが使われます。明示的に呼び出すこともできます。

```text
Use $hsp-script to write a small HSP3 windowed sample.
```

プロンプト例:

```text
HSP3で簡単な時計スクリプトを書いて
```

```text
この .hsp ファイルの構文ミスをレビューして
```

```text
OpenHSPのsample/hsp3dish向けにタッチ入力のサンプルを作って
```

## ファイル構成

- `AGENTS.md`: このskill自体を開発・更新するエージェント向けの方針。
- `skills/SKILL.md`: Codex向けのskill定義と発火条件。
- `skills/references/hsp-notes.md`: HSPの構文メモ、コード例、ランタイム別の注意点、OpenHSPリポジトリの配置メモ。
- `skills/agents/openai.yaml`: skill一覧表示などで使うUIメタデータ。
- `README.en.md`: 英語版README。

## 注意

Codex・Claude Code いずれも、リポジトリ本体ではなく `skills/` ディレクトリがスキルとして読み込まれる構成です。シンボリックリンクの向き先はリポジトリ本体ではなく `hsp-script-skill/skills/` にしてください。
