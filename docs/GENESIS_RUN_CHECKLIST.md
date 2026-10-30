# Genesis 本番実行チェックリスト

## A. 実行前

- [ ] Python 3.10〜3.12 を使用している
- [ ] `pip install -r requirements.txt -r requirements-genesis.txt` が完了
- [ ] headless の場合 `PYOPENGL_PLATFORM=egl` を設定
- [ ] `python -m pytest -q` が全件成功
- [ ] `python test_offline.py` が `pass: true`
- [ ] GPU 使用時は `nvidia-smi` が正常

## B. 1 episode / viewer ありで調整

```bash
python genesis3d/genesis_sort_advanced.py --cpu --vis --episodes 1
```

1. カメラ画像でテーブル全体と workspace が見える。
2. 6物体が個別 component として検出される。
3. overlay の label、confidence、entropy が表示される。
4. Approach 後の再観測で対象が消えない。
5. Descend 時に指先が机へ衝突しない。
6. 把持後、指開き幅と table-clear の両方が成立する。
7. 各ビンの中心へ到達し、リリース後に物体が収まる。

## C. 調整順序

| 症状 | 最初に見る値 | 次に見る値 |
|---|---|---|
| 物体が検出されない | `perception.min_height_m / max_height_m` | camera pose / FOV / table depth |
| 誤分類が多い | confidence / margin / entropy のログ | 合成乱択の強さ、Genesis 画像での追加学習 |
| 3D位置がずれる | camera pose / look_at / up | resolution / FOV と内部行列 |
| 指が届かない・机に当たる | `hand_down_offset_m` | object height / camera depth scale |
| 空振りが多い | closed-loop correction と XY offset | yaw、pre-close 幅、grasp force |
| 運搬中に落ちる | slip ログ、`base_force_n` | friction、motion steps、force limit |
| IK 失敗 | workspace / safe_z | approach_z、bin 座標、Panda 初期姿勢 |

一度に複数値を変えず、seed と変更点を `events.jsonl` と一緒に残してください。

## D. 評価 run

```bash
python genesis3d/genesis_sort_advanced.py --episodes 5
ffmpeg -i out/genesis/genesis_raw.mp4 -c:v libx264 -pix_fmt yuv420p out/genesis/genesis_demo.mp4
```

最低限記録する値:

- objects attempted / succeeded / success rate
- classification accuracy（simulation true label を評価専用に使用）
- mean attempts
- failure distribution
- seed、設定ファイル、モデル

## E. 提出前

- [ ] 1〜3分の動画になっている
- [ ] 2倍速なら動画内または概要欄に明記
- [ ] `README.md` の未確認記述を実測値へ更新
- [ ] PDF の結果欄を `summary.json` の実値へ更新
- [ ] 公開 GitHub URL を確認
- [ ] 個人情報・社内情報・認証情報がないことを確認
