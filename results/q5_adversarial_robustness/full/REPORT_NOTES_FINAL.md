# Question 5 — Automatically Generated Evidence Notes

- Seed: 42
- Execution mode: full
- Datasets: fashion_mnist, cifar10
- Baseline epoch reporting: clean Train/Test loss and accuracy were measured after every baseline epoch. Test values were reporting-only and never used for optimization or selection.
- PGD selection: the complete nine-setting grid used only held-out validation data.
- Defense computational cost: incremental training time, total pipeline time, model storage, incremental training GPU memory, estimated isolated peak GPU memory, and adversarial gradient steps per batch were recorded.
- Dataset-consistent DataLoader batch sizes: {'fashion_mnist': 2048, 'cifar10': 1024}. The configured batch for each dataset is used across all training and evaluation pipelines, and the last incomplete batch is retained.
- EOT-PGD: 10 gradient samples per step, 20 prediction samples, 40 steps, and 3 restarts on the complete official test set.
- AutoAttack: standard suite (APGD-CE, APGD-T, FAB-T, Square) on the complete official test set.
- TCAV: 30 independent references; disjoint classes; clean-correct target examples.

## Model-level numerical evidence

- fashion_mnist / baseline: clean=0.8928, FGSM=0.6660, selected-PGD=0.6343, strong-PGD-40x5=0.6271, EOT-PGD=0.6281, AutoAttack=0.6267, training-time=51.75s, estimated-isolated-peak-GPU=727.38MB; verdict=robustness_supported_by_multiple_attacks.
- fashion_mnist / fgsm_at: clean=0.8865, FGSM=0.7847, selected-PGD=0.7695, strong-PGD-40x5=0.7664, EOT-PGD=0.7668, AutoAttack=0.7642, training-time=33.00s, estimated-isolated-peak-GPU=1190.64MB; verdict=robustness_supported_by_multiple_attacks.
- fashion_mnist / pgd_at: clean=0.8773, FGSM=0.7971, selected-PGD=0.7868, strong-PGD-40x5=0.7854, EOT-PGD=0.7859, AutoAttack=0.7818, training-time=37.72s, estimated-isolated-peak-GPU=688.45MB; verdict=robustness_supported_by_multiple_attacks.
- cifar10 / baseline: clean=0.8076, FGSM=0.0423, selected-PGD=0.0002, strong-PGD-40x5=0.0001, EOT-PGD=0.0001, AutoAttack=0.0001, training-time=476.26s, estimated-isolated-peak-GPU=6781.36MB; verdict=robustness_supported_by_multiple_attacks.
- cifar10 / fgsm_at: clean=0.6764, FGSM=0.3156, selected-PGD=0.2583, strong-PGD-40x5=0.2460, EOT-PGD=0.2455, AutoAttack=0.2169, training-time=525.34s, estimated-isolated-peak-GPU=11383.85MB; verdict=robustness_supported_by_multiple_attacks.
- cifar10 / pgd_at: clean=0.6133, FGSM=0.3701, selected-PGD=0.3482, strong-PGD-40x5=0.3441, EOT-PGD=0.3440, AutoAttack=0.3073, training-time=1051.20s, estimated-isolated-peak-GPU=6854.27MB; verdict=robustness_supported_by_multiple_attacks.

## Corrected TCAV evidence

- fashion_mnist / baseline / target=Ankle boot: concept=footwear, mean sign-count=1.0000, reference=0.0000, p=0, dz=inf.
- fashion_mnist / baseline / target=T-shirt/top: concept=footwear, mean sign-count=0.3349, reference=0.6651, p=0.0182, dz=-0.4570.
- fashion_mnist / pgd_at / target=Ankle boot: concept=footwear, mean sign-count=1.0000, reference=0.0000, p=0, dz=inf.
- fashion_mnist / pgd_at / target=T-shirt/top: concept=footwear, mean sign-count=0.1568, reference=0.8432, p=4.952e-08, dz=-1.3314.
- cifar10 / baseline / target=automobile: concept=vehicle, mean sign-count=0.9667, reference=0.0333, p=1.964e-14, dz=2.5560.
- cifar10 / baseline / target=dog: concept=vehicle, mean sign-count=0.0000, reference=1.0000, p=0, dz=inf.
- cifar10 / pgd_at / target=automobile: concept=vehicle, mean sign-count=1.0000, reference=0.0000, p=0, dz=inf.
- cifar10 / pgd_at / target=dog: concept=vehicle, mean sign-count=0.0000, reference=1.0000, p=0, dz=inf.

## Mandatory interpretation rules

1. Use AutoAttack, EOT-PGD, and strong PGD as the main robustness evidence, not FGSM alone.
2. Explicitly label any model flagged as attack-specific overfitting or gradient masking as an unsuccessful defense.
3. Report both incremental defense fine-tuning time and total pipeline time, together with estimated isolated peak GPU memory.
4. State that baseline test metrics were recorded by epoch only for reporting and were not used for model or attack selection.
5. State that PGD alpha and steps were selected on held-out validation data.
6. Interpret TCAV as sensitivity to a user-defined concept, not as proof of causal reasoning.

All report tables, figures, checkpoints, GPU-memory metadata, EOT artifacts, TCAV artifacts, and readiness checks are stored under the v7 Fashion-2048 / CIFAR-1024 independent-surrogate results directory.