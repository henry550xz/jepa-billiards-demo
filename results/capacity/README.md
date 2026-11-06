# Environment complexity, latent size and predictor capacity

The main question is how a world model’s required latent size and predictor complexity relate to its environment. We built a two-ball 3D world with a 12-coordinate position/velocity state and completed the primary four-size Gaussian capacity sweep. See [the research report](research-report.pdf) for the environment, design, all-setting time/RMSE plots, findings and queued follow-up controls.

Numerical snapshot: November 5, 2026, 22:00:13 EST.
15/24 JEPA encoders, 45/72 frozen predictors, 30/48 readouts and all nine true-state controls complete. Gaussian covers L6/12/24/48; Sparse currently covers L6. Larger Sparse codes and three supervised image-state references are pending.

Each encoder received 20,000 updates. Three frozen predictors (affine, MLP-64, MLP-256) received 10,000 updates each. Aggregate charts use all 256 held-out episodes and all three training seeds. H32 is 1.28 seconds. Means are arithmetic means of seed-specific metrics, not confidence intervals.

Playback uses the first three test episodes in manifest order, fixed without selecting by model error. Original three-frame image inputs are exported directly from retained RGB arrays. Recorded forecast coordinates are rounded to nine significant digits for display; reported scientific metrics retain their saved precision. The box view stays fixed, and out-of-box/overlapping decoded states are flagged rather than clamped. These are physical-state readout trajectories, not generated RGB or browser inference. Actual-future readouts use future images and are a diagnostic rather than a forecast.

Each curated encoder JSON includes every completed predictor, both state readouts, aggregate position/velocity metrics at the plotted horizons, native MSE and three fixed playback clips. Missing blocks are pending, not zero or failed results. Large finite errors and all seeds are preserved. True-state persistence, learned state controls and exact physics have privileged state inputs; they do not isolate visual encoding from dynamics.

The observed Gaussian L12 comparison shows lower one-step feature MSE for the MLPs alongside seed-sensitive long-rollout instability. Nearly equal Gaussian affine position errors across latent sizes do not establish useful compactness. Velocity improvements must be stated separately from position, and the incomplete matrix does not support an objective-wide winner or dimensional-sufficiency claim.

Original experiment source: `968e6a825be49d662f303cf630315024f2f86d33`. Numerical snapshot SHA256: `21fe079122d3decc68e57b6e51004abb439a26726aebedb5e6a59aba025b844a`. Dataset-manifest and exported per-encoder hashes appear in index.json. Completed checkpoints, cache provenance and predictor forecasts were verified before export; physical aggregate metrics were independently recomputed from retained forecasts.

Scientific protocol/code: https://github.com/henry550xz/jepa-worldmodel-comparison/blob/main/docs/BILLIARDS_CAPACITY_PROTOCOL.md

The primary Gaussian sweep is complete; representation-family checks and supervised references extend its interpretation. This is a static scientific snapshot, not a live GPU connection. No new training, inference or protocol modification was performed for publication.

The visual-aid export omits detailed representation diagnostics, event-stratified metrics, full per-episode errors, checkpoints and training data. Only aggregate curves, three fixed example clips and their input montages are included.
