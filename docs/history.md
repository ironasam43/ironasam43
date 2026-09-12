# 変更履歴

> ⚠️ 2026-06-25: HQ の操作ミス（破壊的一括 mv）により、本ファイルの旧内容が消失した可能性があります。
> 当時このファイルは git 未追跡で機械復旧できず、アーカイブ（history_1.md）も存在しませんでした。
> 元の内容は空またはスタブだった可能性が高いものの、断定はできません。
> 以降は本ファイルを git 追跡対象とし、再発を防止します。

## 2026-08-13
- `deeperai/support.md`（DeeperAI アプリが実行時に fetch する AI 向け ground truth）を更新。**SETUP-001「Claude Code CLI の導入手順」を Section 4 として新設**（Homebrew → `brew install --cask claude-code` → `claude` で認証 → DeeperAI 側「AI 実行モード」/「ローカルCLI連携（keyless）」の設置/「CLIエンジン」/「再検出」→ `claude doctor` によるトラブルシューティング。ja/en 併記）。あわせて 1.3.8 前提だった既存記述を実装の現状へ追随（ヘッダを 1.5.0 App Store / 2.0.0 開発中へ・ISSUE-001/002 に `status: resolved`・FAQ-001 を APIキー/Keyless CLI の2方式併記へ・FAQ-004 を方式別の切り分けへ・**FAQ-006（Keyless CLI とは）新設**・BEH-003 をキャンペーン終了済みへ・BEH-004 をプラン体系（無料 25,000 / 月額 100万・月 / 買い切り 無制限）へ・**BEH-005（Keyless CLI 30日お試し）新設**）。出荷済み 1.5.0 も本ファイルを読むため、Keyless 関連は `affects: v2.0.0+ (macOS)` で版差を明示した。価格は App Store 表示を正本として記載しない方針を本文に明記。

- **GitHub Pages のビルド失敗を修復（remote ロールバック）**。上記 support.md 更新の push に、6月から未 push で滞留していた HQ の housekeeping コミット4本が同時に上がり、そこに含まれる**壊れた symlink**（`docs/cmflow.md` / `docs/verify-queue.template.md` → Dev ワークスペース側の実体を指すため clone 先では解決不能）を Jekyll が realpath 解決できずビルド全体がクラッシュした（run `31652012273`・`build failed` / `deploy skipped`）。**Human 裁定により remote を最終グリーンの `5e620d1` へ force-push でロールバック**（support.md の更新も 2.0 リリースまで remote には出さない）。ロールバック後の run `31654332957` で **build success / deploy success** を確認し、`legal/{eula,privacy,terms,tokusho}.html`・`deeperai/privacy.html`・サイトルート（`https://ironasam43.github.io/ironasam43/`）の 200 疎通を機械確認。
- 再発防止の修正を**ローカルコミットのみで保持**（**2.0 リリース後に push する**）。①壊れた symlink 2本と `.DS_Store` を `git rm --cached` で追跡解除（作業ツリーの symlink 実体はローカル運用に必要なので残置）②`.gitignore` を新規作成して再混入を防止 ③`_config.yml` を追加し、`theme: jekyll-theme-primer`（現行の暗黙既定と同一。公開中ページが `container-lg px-3 my-5 markdown-body` で描画されていることで確認）を明示固定したうえで `exclude` に `docs` / `CLAUDE.md` / `.devdeck.json` を指定し開発用ドキュメントを公開サイトから除外。**これらは push していないため Pages 上での検証は未了**——2.0 リリース後の push 時に Pages ビルド成功と legal ページ 200・見た目維持を必ず確認すること。

## 2026-06-25
- `docs/verify-queue.template.md` を Dev/docs から相対 symlink で配布（全PJ完全パリティ・HQ 直接改修）。
- 本 history.md を git 追跡対象に追加（従来は未追跡だった）。
