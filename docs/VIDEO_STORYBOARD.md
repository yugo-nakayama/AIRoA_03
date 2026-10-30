# 提出動画ストーリーボード（約100〜130秒）

| 時間 | 映像 | テロップ／説明 |
|---:|---|---|
| 0〜8秒 | 完成動作のハイライト | AI Shape Sorting Robot Arm - Advanced / Genesis + Franka Panda + RGB-D |
| 8〜22秒 | シーン全景と上方画像の2画面 | 6物体、3クラス、3ビン。色ではなく深度シルエットから形を判定 |
| 22〜40秒 | overlay を拡大 | MLP予測だけでなく confidence / margin / entropy を算出。曖昧ならつかまない |
| 40〜58秒 | Approach 後の再観測 | 動作直前に対象を再検出し、位置ずれを補正する closed-loop perception |
| 58〜78秒 | Descend、pre-close、force grasp、lift | 衝撃を減らす段階把持。指開き幅 + RGB-D table-clear の二重判定 |
| 78〜96秒 | 意図的な失敗または再試行 | 空振り、slip、IK failure を区別し、offset / yaw / force / retreat を変更 |
| 96〜112秒 | 3クラスが各ビンへ置かれる | 形状に対応したビンへ仕分け。true label は評価だけに使用 |
| 112〜126秒 | summary JSON / 簡単な表 | 成功率、平均試行数、失敗分布、seed を自動記録 |
| 126〜130秒 | 終了画面 | Code: public GitHub repository |

## 撮影時の要点

- 画面左: 側面カメラ、右: 上方 RGB-D overlay、下: 現在状態。
- `uncertain_class -> defer` と `empty_grasp -> recovery` のどちらかを1回見せると上級編の意義が伝わりやすい。
- 倍速を使う場合は冒頭または画面右上に「2x speed」を常時表示。
- 最後の結果は、事前に作った架空値ではなく実行後の `summary.json` を使用する。
