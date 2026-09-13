# プロジェクトガイドライン

このファイルは AI コーディングエージェント向けの共通指示を記載する。

## このリポジトリが扱うもの

UI の画面の構造（まとまりと優先順位）に関する UX 規則をチェックし適用するエージェントスキル `ux-structure-review` を管理する。
スキルの形式は Claude Code と Codex で共通であり、どちらか一方に依存する記述を入れない。
スキル本体は `skills/ux-structure-review/` にあり、利用者はこのディレクトリを使うエージェントのスキルディレクトリへコピーして使う。

同じ立ち位置の姉妹スキルが三つある。

- `ux-state-review`：UI の状態（待つ、空、失敗、権限不足、削除、完了、入力不備）
- `ux-readability-review`：文字と文言（読みやすさ）
- `ux-load-review`：記憶、判断、操作の負担

姉妹スキルの範囲に入る話題はそちらに譲り、このスキルでは扱わない。

## 言語

日本語を共通言語とする。応答、コミットメッセージ、Pull Request、Issue、ドキュメントはすべて日本語で書く。
文書を書く、または推敲するときは `/japanese-tech-writing` スキルの文章規範に従う。

## スキルを編集するときの原則

- スキルは単体で意味が通るように書く。作成の経緯、参考にした資料や画像、過去の会話に言及しない。読む側にはそれらが存在しない。
- 守るのは規則とその目的であり、特定の見た目ではない。文言や画面構成の例を到達目標として書かない。
- 「対象外」と「別の表現で満たす条件」を混ぜない。前者はその構造が存在しないか、存在しても利用者が区別や優先順位を必要としない場合、後者は別の手段で目的を達成できる場合である。
- 規則の一覧表は `skills/ux-structure-review/SKILL.md` と `README.md` の両方にある。片方を変えたらもう一方も揃える。
- 規則を変更したら `skills/ux-structure-review/evals/evals.json` に、その変更を検証できるテストプロンプトを追加する。

## AI クロスレビュー

実装を一区切りしたら、`docs/cross-review.md` の手順で相互レビューを行う。
実行は `npm run review:codex`（Codex がレビュー）または `node tools/cross-review.js subagent`（CLI を使えない環境）を使う。
レビュー観点はリポジトリ直下の `.cross-review.md` にある。
`tools/`、`docs/cross-review.md`、`.cross-review.example.md`、`.claude/skills/cross-review/SKILL.md` は upstream からの同期対象であり、直接編集せず `npm run sync` で更新する。
