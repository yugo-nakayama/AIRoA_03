# Changelog

## 2.0.0 - Advanced Genesis 3D Edition

- Added geometry-augmented silhouette MLP and morphology test-time augmentation.
- Added confidence margin, normalized entropy, depth MAD and explicit rejection.
- Replaced axis guessing with pinhole back-projection using `T_world_cam`.
- Added approach-stage re-observation and target association.
- Added staged gripper close, dual grasp verification and slip check.
- Added failure-specific bounded recovery.
- Added JSONL telemetry, summary metrics, tests, report and video storyboard.
- Preserved an explicit boundary: offline components verified; Genesis physics run pending.
