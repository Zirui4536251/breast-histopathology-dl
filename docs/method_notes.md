# Method and editorial notes

## Original experiment

An ImageNet-pretrained ResNet-18 was adapted for normal-versus-invasive-carcinoma image classification. Its new head is Dropout(0.5), Linear(512, 256), ReLU, Dropout(0.3), Linear(256, 2). Training uses cross-entropy, AdamW and cosine annealing, with batch size 16, a maximum of 25 epochs and early-stopping patience 5. The saved CPU run stopped at epoch 18.

The initial learning rate is 1e-4. After epoch index 5, internal validation accuracy above 0.8 triggers unfreezing of layer3 and layer4 and a new optimizer at 1e-5. As implemented, this optimizer/scheduler reset can happen repeatedly, not just once. The source training logic is retained for traceability.

## Qualifications that matter when interpreting results

1. **Augmentation was defined but overwritten.** `random_split` produces two subsets referencing one dataset. Assigning `val_subset.dataset.transform = val_transform` also changes the training subset's transform. The saved run therefore cannot be described as using the defined random flips, rotation and colour jitter. Correcting this would require a new experiment and new results.
2. **Frozen parameters do not freeze BatchNorm statistics.** Calling `model.train()` still updates running statistics in the backbone, even when its parameter gradients are disabled.
3. **Internal reporting and checkpoint selection differ.** The best checkpoint is restored, but the final internal report uses predictions collected during the last epoch. The separate 82-image validation block evaluates the restored model.
4. **Image-level splits are not patient-level validation.** No patient or slide identifiers are available in the reviewed materials. The 82-image course set is not evidence of external clinical validation.
5. **Grad-CAM is illustrative.** The four examples come from the original training directory, not a dedicated held-out explanation set. Heatmaps show contributions to a class score; they do not establish tumour segmentation, causal features, or pathologist-confirmed localization. Displayed softmax values are not confidence intervals or calibrated clinical probabilities.
6. **Reproducibility is incomplete.** Original library versions, raw images and checkpoint are absent. Seeds are set, but directory listings are not sorted before the training split or Grad-CAM example selection. A new environment may change the split and results. The retained backward-hook API is deprecated and may need adaptation.

## Changes made for this repository

- Split the original large cells into named sections, removed redundant screenshots, submission instructions and repetitive comments, and added concise English explanations.
- Replaced machine-specific paths with paths relative to the repository. Future generated files are separated from archived results.
- Kept the original model, training loop, split and Grad-CAM calculations. Did not silently repair the augmentation or scheduler behavior and present the old results as a corrected experiment.
- Made the inference/Grad-CAM stage explicitly use CPU, matching the recorded run and avoiding the original GPU/input-device mismatch.
- Changed test-image failures from silently emitting class 0 to raising an error. No such failures are reported in the archived test output.
- Removed global warning suppression, an inaccurate layer-count explanation, and unsupported claims about specific histological structures. Relabeled displayed softmax values as predicted-class probabilities.
- Extracted existing PNGs without altering their bytes and transcribed existing metrics and predictions. Original console output is retained separately.
- Cleared execution counts and code outputs in the edited notebook. Archived figures are shown in clearly labeled Markdown sections, not attached to changed code as if freshly executed.

Only syntax, file structure, references and archived-output consistency were checked. No notebook cells, model training or inference were executed during this revision. Dependencies are listed without invented version pins; end-to-end execution has not been verified.
