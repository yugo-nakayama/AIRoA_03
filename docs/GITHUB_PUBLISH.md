# GitHub 公開手順

リポジトリ URL はまだ決まっていないため、以下では `<REPOSITORY_URL>` を作成後の URL に置き換えます。

```bash
cd AI_Shape_Sorting_Robot_Arm_Advanced
git init
git branch -M main
git add .
git commit -m "Add advanced Genesis RGB-D shape sorting project"
git remote add origin <REPOSITORY_URL>
git push -u origin main
```

GitHub 側の確認:

1. Visibility が **Public**。
2. README の先頭で目的、実行方法、検証済み／未検証が分かる。
3. `report/AI_Shape_Sorting_Robot_Arm_Advanced_Report.pdf` をブラウザで開ける。
4. `models/shape_mlp_advanced.joblib` が GitHub の通常ファイル上限以内。
5. commit 後に `git status` が clean。
6. 氏名、所属、メール、token、社内情報が含まれていない。
7. Genesis 実行後は README と PDF の「未確認」を実測結果へ更新して再 commit。

提出フォームにはリポジトリのトップ URL を記載します。ZIP の URL や個別ファイル URL ではありません。
