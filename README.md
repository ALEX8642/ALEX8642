# Alexander Feht

Manufacturing & supplier-quality engineer building hands-on ML for semiconductor
quality problems. Everything below is built on public data — the methods travel,
the IP doesn't.

## Semiconductor ML portfolio

| Repo | What it shows | Headline |
|---|---|---|
| [wafer-defect-classifier](https://github.com/ALEX8642/wafer-defect-classifier) | 9-class wafer-map defect classification on WM-811K — focal loss + CBAM attention, temperature-scaled calibration, Grad-CAM++ localization, cost-of-quality analysis, one-click Gradio demo | test macro-F1 **0.92** |
| [wafer-ssl](https://github.com/ALEX8642/wafer-ssl) | SimCLR self-supervised pretraining on 638k unlabeled maps + 4-seed ensemble, with a controlled ablation attributing the gain | test macro-F1 **0.94** |

<p align="center">
  <img src="https://raw.githubusercontent.com/ALEX8642/wafer-defect-classifier/master/assets/gradcam_scratch.png" width="32%" alt="Grad-CAM localizing a scratch defect"/>
  <img src="https://raw.githubusercontent.com/ALEX8642/wafer-defect-classifier/master/assets/gradcam_edge_ring.png" width="32%" alt="Grad-CAM localizing an edge-ring defect"/>
  <img src="https://raw.githubusercontent.com/ALEX8642/wafer-defect-classifier/master/assets/reliability_diagram.png" width="32%" alt="Reliability diagram after temperature scaling"/>
</p>

### How I work — the part the numbers don't show

- **Honest numbers over headline numbers.** Negative results stay in the docs:
  pseudo-labeling regressed the tail classes and was rolled back; a
  focal-loss/class-weights interaction bug is written up as a post-mortem, not
  hidden.
- **Operating points over accuracy.** Escapes and false alarms are priced
  separately (10:1 cost ratio); per-class thresholds move along that trade-off
  curve, and calibration (ECE 0.016 → 0.003) makes confidence something you can
  route on.
- **Attribution over vibes.** The self-supervised result ships with a
  from-scratch ensemble control: +1.8pp from ensembling, +0.8pp from
  pretraining — measured, not assumed.
- **Explainability a fab can use.** Grad-CAM++ overlays tie each prediction to
  the process signature a quality engineer would recognize — edge-ring
  uniformity effects, scratch arcs, center chuck marks — with a defect-class →
  process-failure-mode mapping in the docs.

### In progress

- **wafer-mixed** — robustness study on MixedWM38: multi-label classification of
  mixed (superposed) defect patterns, plus a transfer study from the WM-811K
  backbones.
- **Root-cause analytics** — classifier outputs joined to a simulated MES/SQL
  schema for spatial-signature → tool attribution.
- **Deployment & drift monitoring** — model serving with input-drift detection
  and calibration-decay tracking.

### Also here

Local-first LLM infrastructure: [audio2report](https://github.com/ALEX8642/audio2report)
(meeting audio → deduplicated transcripts → audit reports, fully offline) and
[LLM-chatbot](https://github.com/ALEX8642/LLM-chatbot) (RAG over technical
manuals with Haystack + Ollama).
