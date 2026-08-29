Paper 1:
Title:

Dual-Critic Uncertainty-Gated Reinforcement Learning for Vision-Dropout-Robust Image-Based Visual Servoing

Abstract:

Image-based visual servoing assumes a steady camera feed, but real eye-in-hand systems do not: occlusion, network jitter, and sensor faults interrupt vision while joint encoders keep working. We study this under a two-state Markov dropout channel with DCUG-PPO, whose actor blends with a model-based fallback — robot kinematics plus an αβ-filter target estimate — through a gate trained directly by the policy objective, no separate loss. Across ten training seeds and three dropout severities, DCUG-PPO reaches 91.4±3.8% success at moderate dropout, ahead of a classical fallback controller (68.0%) and a matched single-critic baseline (83.1±29.3%) that collapses entirely in one of ten runs, a failure DCUG-PPO never shows. TD3, a stronger off-policy method, scores higher still (98.7±1.2%) without collapsing, at roughly five times the control effort and forty times the jerk. We keep the claim narrow: the gains hold against on-policy training, and DCUG-PPO is the smoothest learned controller tested — though a bare no-fallback baseline is smoother yet, mostly by freezing its output through each dropout rather than steering through it. Seed-level tests against the single-critic baseline miss significance at n=10; what survives is qualitative — one collapse in ten runs, none elsewhere — and it holds zero-shot across three simulation tiers: idealized kinematics, MuJoCo rigid-body dynamics, and rendered images processed through OpenCV. We report results plainly: where TD3 wins, where the ablation narrows, and what is missing — no physical robot, no test against SAC, PPO-LSTM, Dreamer, or distributional RL.

Keywords:

image-based visual servoing, reinforcement learning, proximal policy optimization, sensor dropout, uncertainty-aware control, dual-critic learning, eye-in-hand robotics

Paper 2 Extension:
Title: Does Fallback-Anchored Uncertainty Gating Help Off-Policy Reinforcement Learning? A Short Study Combining DCUG-Style Gating with TD3

Abstract:
Our companion paper proposed DCUG-PPO, which anchors an on-policy PPO actor to a model-based fallback controller through a learned uncertainty gate, and found that this fixes a specific training-collapse failure mode in on-policy learning for image-based visual servoing under intermittent camera dropout. That paper also found that TD3, an off-policy algorithm with no such anchoring, matches or exceeds DCUG-PPO’s raw performance and shows no collapse across the seeds tested, and explicitly left open whether fallback-anchoring and off-policy replay-buffer training are complementary or redundant routes to reliability. This paper answers that question directly: we implement DCUG-TD3, applying the identical fallback-anchoring and dual-critic gating mechanism to TD3’s deterministic policy, and train and evaluate it across ten seeds under the same protocol; we also retrained vanilla TD3 from three to ten seeds so both methods are compared with matched statistical power. The result is a clean negative one: DCUG-TD3 is statistically indistinguishable from vanilla TD3 on success rate at every severity (p = 0.22–0.96), shows no improvement in control smoothness, and the learned gate converges to a mean value of α = 0.85 ± 0.16 – mostly trusting the raw policy rather than the fallback. We interpret this as evidence that fallback-anchoring’s benefit is specific to the on-policy training-collapse mode it was designed to fix, not a general-purpose robustness booster that stacks with any base algorithm. We report this null result in full, because it clarifies that the companion paper’s mechanism is not simply "always helpful" and sharpens what it actually does.

Keywords: reinforcement learning, TD3, uncertainty-aware control, off-policy learning, ablation study, image-based visual servoing
