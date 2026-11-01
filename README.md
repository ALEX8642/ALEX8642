# Alexander Feht

Quality engineer (ASQ-CQE, 15+ years in regulated hardware manufacturing) who deploys and operates
private LLM infrastructure: multi-node serving, evaluation gates, silent-failure monitoring and
disaster recovery, run with the same discipline as a production line.

I build with AI coding agents (Claude Code, Codex, GitHub Copilot CLI). I set the architecture,
constraints and acceptance criteria, then review, test, deploy and operate what they write.

## On-prem LLM deployment & evaluation

| Repo | What it shows |
|---|---|
| [onprem-llm-stack](https://github.com/ALEX8642/onprem-llm-stack) | Two NVIDIA GB10 nodes serving large quantized models (MiniMax M2.7, Qwen3.5-122B, Qwen3.8-Flash-Next) tensor-parallel on vLLM / SGLang / Atlas, behind a LiteLLM gateway and OpenWebUI with SSO. Includes an A/B evaluation harness that caught a faster recipe failing long-context retrieval, a watchdog for a silent NaN-logits fault (detect → contain → correct → escalate), an Ansible rebuild with a written DR runbook, a measured trial of Cohere Command A+ (218B MoE, TP=2), and a tool-call eval of the Home Assistant voice agent |
| [audio2report](https://github.com/ALEX8642/audio2report) | Dual-mic meeting recordings → deduplicated transcript → LLM audit report, fully local (WhisperX, pluggable local LLM backends, CPU/GPU Docker images, CI). A work version has been used on four audits |
| [LLM-chatbot](https://github.com/ALEX8642/LLM-chatbot) | RAG over PDF manuals: hybrid retrieval (Qdrant dense + OpenSearch BM25, reciprocal-rank fusion) and cross-encoder reranking, with Cohere Command R7B via Ollama and page-level citations |

## ML lifecycle on public data

| Repo | What it shows | Headline |
|---|---|---|
| [wafer-defect-classifier](https://github.com/ALEX8642/wafer-defect-classifier) | 9-class WM-811K wafer maps: focal loss + CBAM, temperature-scaled calibration, Grad-CAM++ | macro-F1 **0.92**, ECE 0.003 |
| [wafer-ssl](https://github.com/ALEX8642/wafer-ssl) | SimCLR pretraining on 638k unlabeled maps + 4-seed ensemble, with an ablation attributing the gain | macro-F1 **0.94** |
| [wafer-mixed](https://github.com/ALEX8642/wafer-mixed) | Multi-label mixed-defect classification (MixedWM38), transfer study, cost-weighted per-label thresholds | macro-F1 **0.98** |
| [wafer-rootcause](https://github.com/ALEX8642/wafer-rootcause) | Simulated MES in DuckDB; SQL commonality analysis (z-tests + BH-FDR) recovers planted equipment faults | precision@1 **~0.9–1.0** |
| [wafer-deploy](https://github.com/ALEX8642/wafer-deploy) | FastAPI serving with a bit-for-bit parity test, three drift monitors, hysteresis retrain trigger, Prometheus + Grafana | scored detection latency and false-alarm rate |

Negative results stay in the docs. For example, a pseudo-labeling regression was rolled back and a
loss-function bug is written up as a post-mortem.
