# Awesome Mamba for Time Series

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/tamlhp/awesome-mamba-ts?style=social)](https://github.com/tamlhp/awesome-mamba-ts/stargazers)
![visitors](https://visitor-badge.laobi.icu/badge?page_id=tamlhp.awesome-mamba-ts)
<img src="https://img.shields.io/badge/Contributions-Welcome-278ea5" alt="Contrib"/>

A living index of academic papers, implementations, datasets, benchmarks, and practical guidance for **Mamba and selective state space models for time-series forecasting**.


- [Taxonomy](#taxonomy)
- [Foundations and Baselines](#foundations-and-baselines)
- [Pure Selective-SSM Forecasters](#pure-selective-ssm-forecasters)
- [Bidirectional and Multi-Directional Scans](#bidirectional-and-multi-directional-scans)
- [Hybrid Architectures](#hybrid-architectures)
- [Specialized Designs](#specialized-designs)
- [Implementation Registry](#implementation-registry)
- [Performance Comparison](#performance-comparison)
- [Datasets and Benchmarks](#datasets-and-benchmarks)
- [Evaluation Metrics](#evaluation-metrics)
- [Practical Guidelines](#practical-guidelines)
- [Contributing](#contributing)

<!-- ## Citation

If you use this repository, please cite the survey manuscript. A public DOI or finalized venue entry will be added once the paper metadata is finalized.

```bibtex
@misc{pham2026mamba-time-series,
  title = {Mamba for Time Series: A Contemporary Survey},
  author = {Anonymous Authors},
  year = {2026},
  note = {Survey manuscript},
  url = {https://github.com/tamlhp/awesome-mamba-ts}
}
```
-->

## Taxonomy

![Roadmap timeline of Mamba-based time-series forecasting methods](figs/mamba-ts.png)

Mamba-based time-series forecasting methods involve pure selective-SSM, bidirectional/multi-directional, and hybrid tracks with key design axes:

- **Tokenization**: pointwise, patch, channel-as-token, event-token, or multi-scale tokenization.
- **Channel strategy**: channel-independent (CI), channel-dependent/channel-mixing (CD), channel-correlated (CC), or dual time/channel mixers.
- **Directional scan**: forward-only, bidirectional, multi-scale parallel, or 2D joint-axis selective scans.
- **Hybridization**: pure Mamba, Mamba + attention, Mamba + MLP/EinFFT, Mamba + CNN/convolution, or Mamba + decomposition.
- **Decomposition**: none, trend-seasonal, multi-scale, Fourier/frequency, or cross-domain time-frequency decomposition.


## Foundations and Baselines

These papers define the SSM lineage, Mamba backbone, and time-series baselines used throughout the survey.

| Paper | Year | Category | Venue / Source | Code |
| --- | --- | --- | --- | --- |
| [HiPPO: Recurrent Memory with Optimal Polynomial Projections](https://arxiv.org/abs/2008.07669) | 2020 | SSM foundation | NeurIPS | - |
| [Efficiently Modeling Long Sequences with Structured State Spaces](https://arxiv.org/abs/2111.00396) | 2022 | S4 / structured SSM | ICLR | - |
| [Simplified State Space Layers for Sequence Modeling](https://arxiv.org/abs/2208.04933) | 2023 | S5 / simplified SSM | ICLR | - |
| [Mamba: Linear-Time Sequence Modeling with Selective State Spaces](https://arxiv.org/abs/2312.00752) | 2023 | Selective SSM | arXiv | [Code](https://github.com/state-spaces/mamba) |
| [Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality](https://arxiv.org/abs/2405.21060) | 2024 | Mamba-2 / SSD | ICML | [Code](https://github.com/state-spaces/mamba) |
| [Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting](https://arxiv.org/abs/2012.07436) | 2021 | Efficient Transformer baseline | AAAI | [Code](https://github.com/zhouhaoyi/Informer2020) |
| [Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting](https://arxiv.org/abs/2106.13008) | 2021 | Decomposition Transformer baseline | NeurIPS | [Code](https://github.com/thuml/Autoformer) |
| [A Time Series is Worth 64 Words: Long-Term Forecasting with Transformers](https://arxiv.org/abs/2211.14730) | 2023 | Patch Transformer baseline | ICLR | [Code](https://github.com/yuqinie98/PatchTST) |
| [iTransformer: Inverted Transformers Are Effective for Time Series Forecasting](https://arxiv.org/abs/2310.06625) | 2024 | Channel-as-token baseline | ICLR | [Code](https://github.com/thuml/iTransformer) |
| [Are Transformers Effective for Time Series Forecasting?](https://arxiv.org/abs/2205.13504) | 2023 | Linear baseline | AAAI | [Code](https://github.com/cure-lab/LTSF-Linear) |
| [N-BEATS: Neural Basis Expansion Analysis for Interpretable Time Series Forecasting](https://arxiv.org/abs/1905.10437) | 2020 | MLP / basis expansion baseline | ICLR | - |
| [N-HiTS: Neural Hierarchical Interpolation for Time Series Forecasting](https://arxiv.org/abs/2201.12886) | 2023 | Multi-rate baseline | AAAI | [Code](https://github.com/Nixtla/neuralforecast) |
| [TimesNet: Temporal 2D-Variation Modeling for General Time Series Analysis](https://arxiv.org/abs/2210.02186) | 2023 | 2D temporal baseline | ICLR | [Code](https://github.com/thuml/TimesNet) |
| [Reversible Instance Normalization for Accurate Time-Series Forecasting Against Distribution Shift](https://arxiv.org/abs/2103.01098) | 2022 | Normalization | ICLR | [Code](https://github.com/ts-kim/RevIN) |

## Pure Selective-SSM Forecasters

Pure forecasters replace the main forecasting backbone with Mamba or a closely related SSM block, usually with RevIN preprocessing and a linear prediction head. They are the strongest starting point when the lookback window is long and stable cross-channel structure is weak.

| Paper / Method | Year | Category | Venue / Source | Code |
| --- | --- | --- | --- | --- |
| [Mamba Time Series Forecasting with Uncertainty Quantification](https://doi.org/10.1088/2632-2153/adec3b) | 2025 | Patch-based pure SSM; probabilistic head | MLST | [Code](https://github.com/PessoaP/Mamba-ProbTSF) |
| [RLMamba: Integrating Residual Learning With Mamba for Long-Term Time Series Forecasting](https://doi.org/10.1016/j.eswa.2025.127362) | 2025 | Residual pure SSM | Expert Systems with Applications | announced |
| [FedRMamba: Federated Residual Mamba for Multivariate Time-Series Forecasting](https://doi.org/10.1145/3774904.3792712) | 2025 | Federated residual Mamba | WWW Companion | announced |
| [GCMNet: A Global Context Mamba Network for Long-Term Time Series Forecasting](https://doi.org/10.1016/j.patcog.2026.113287) | 2026 | Global-context pure SSM | Pattern Recognition | announced |
| [Is Mamba Effective for Time Series Forecasting? / S-Mamba](https://arxiv.org/abs/2403.11144) | 2025 | Channel-as-token pure SSM | Neurocomputing | [Code](https://github.com/wzhwzhwzh0921/S-D-Mamba) |
| [Is Mamba Effective for Time Series Forecasting?](https://arxiv.org/abs/2403.11144) | 2024 | Negative / protocol study | Neurocomputing | [Code](https://github.com/wzhwzhwzh0921/S-D-Mamba) |
| [MambaTS: Improved Selective State Space Models for Long-Term Time Series Forecasting](https://arxiv.org/abs/2405.16440) | 2024 | VAST learned scan order | arXiv | [Code](https://github.com/XiudingCai/MambaTS-pytorch) |
| [SAMBA: Simplified Mamba with Disentangled Dependency Encoding for Long-Term Time Series Forecasting](https://arxiv.org/abs/2408.12068) | 2024 | Gate-free Mamba block | arXiv | [Code](https://github.com/mshliang/SAMBA) |
| [DTMamba: Dual Twin Mamba for Time Series Forecasting](https://arxiv.org/abs/2405.07022) | 2024 | Dual forward/reverse pure SSM | arXiv | [Code](https://github.com/lizyelon/DTMamba) |
| [TimeMachine: A Time Series is Worth 4 Mambas for Long-Term Forecasting](https://arxiv.org/abs/2403.09898) | 2024 | Multi-scale pure SSM | ECAI | [Code](https://github.com/Atik-Ahamed/TimeMachine) |
| [SiMBA-TS: Simplified Channel Mixing and Mamba for Long-Term Time Series Forecasting](https://ieeexplore.ieee.org/document/10890315) | 2024 | Patch-based pure SSM with channel mixer | arXiv | [Code](https://github.com/badripatro/Simba) |
| [C-Mamba: Channel Correlation Enhanced State Space Models for Multivariate Time Series Forecasting](https://arxiv.org/abs/2406.05316) | 2024 | Channel-correlation graph | arXiv | [Code](https://github.com/chenhan-y/C-Mamba) |
| [CMamba: Channel Correlation Enhanced State Space Models for Multivariate Time Series Forecasting](https://arxiv.org/abs/2406.05316) | 2024 | Global cross-channel mixer | arXiv | [Code](https://github.com/zshhans/CMamba) |
| [CMMamba: Channel Mixing Mamba for Time Series Forecasting](https://doi.org/10.1186/s40537-024-01001-9) | 2024 | Channel-mixing Mamba | Journal of Big Data | announced |
| [MambaStock: Selective State Space Model for Stock Prediction](https://arxiv.org/abs/2402.18959) | 2024 | Finance pure SSM | arXiv | [Code](https://github.com/zshicode/MambaStock) |
| [DGMamba: Domain Generalization via Generalized State Space Model](https://arxiv.org/abs/2404.07794) | 2024 | Domain-generalized Mamba | ACM MM | [Code](https://github.com/longshaocong/DGMamba) |
| [Mamba4Cast: Efficient Zero-Shot Time Series Forecasting with State Space Models](https://arxiv.org/abs/2410.09385) | 2024 | Zero-shot / foundation-style Mamba | arXiv | [Code](https://github.com/automl/mamba4cast) |
| [Effectively Modeling Time Series with Simple Discrete State Spaces](https://arxiv.org/abs/2303.09489) | 2023 | Pre-Mamba SSM foundation forecaster | ICLR | [Code](https://github.com/HazyResearch/spacetime) |

## Bidirectional and Multi-Directional Scans

This branch modifies Mamba's native unidirectional scan. Bidirectional scans improve context symmetry for forecasting, while multi-scale and 2D scans target long-horizon or high-channel multivariate data.

| Paper / Method | Year | Category | Direction / Fusion | Venue / Source | Code |
| --- | --- | --- | --- | --- | --- |
| [ms-Mamba: Multi-scale Mamba for Time-Series Forecasting](https://arxiv.org/abs/2504.07654) | 2025 | Multi-scale scan | Parallel scans + MLP | arXiv | [Code](https://github.com/airin/ms-Mamba) |
| [BiG-Mamba: Bidirectional Graph and Mamba Modeling for Multivariate Time Series Forecasting](https://doi.org/10.1007/978-981-96-9946-9_26) | 2025 | Graph bidirectional scan | Forward + reverse + graph attention | LNCS / Springer | announced |
| [Hierarchical Information-Guided Spatio-Temporal Mamba for Stock Time Series Forecasting](https://arxiv.org/abs/2503.11387) | 2025 | Spatio-temporal bidirectional Mamba | Spatial + temporal scans | Information Sciences | announced |
| [Decomposed Multi-Scale Temporal-Channel Interaction with Bidirectional Mamba for Multivariate Time Series Forecasting](https://doi.org/10.2139/ssrn.5382999) | 2025 | Decomposed multi-scale bidirectional Mamba | Trend/seasonal branches | SSRN | announced |
| [Bi-Mamba4TS: Bidirectional Mamba for Time Series Forecasting](https://arxiv.org/abs/2404.15772) | 2024 | Symmetric bidirectional scan | Forward + reverse concat | arXiv | [Code](https://github.com/llwwqq/Bi-Mamba) |
| [Bi-Mamba+: Bidirectional Mamba for Time Series Forecasting](https://arxiv.org/abs/2404.15772) | 2024 | Bidirectional scan with SRA module | Forward + reverse concat | arXiv | [Code](https://github.com/llwwqq/Bi-Mamba-plus) |
| [Bi-Mamba: Bidirectional Mamba for Time Series Forecasting](https://arxiv.org/abs/2404.15772) | 2024 | Univariate bidirectional variant | Shared encoder + projection | arXiv | [Code](https://github.com/llwwqq/Bi-Mamba) |
| [Channel Independence Bidirectional Gated Mamba With Interactive Recurrent Mechanism for Time Series Forecasting](https://doi.org/10.1109/TIE.2025.3581279) | 2024 | Bidirectional gated Mamba | Interactive recurrent gate | Neurocomputing | [Code](https://github.com/CIBGM/CIBGM) |
| [Mamba Meets Financial Markets: A Graph-Mamba Approach for Stock Price Prediction](https://arxiv.org/abs/2410.03707) | 2024 | Graph bidirectional Mamba | Forward + reverse + graph conv | arXiv | [Code](https://github.com/Ali-Meh619/SAMBA) |
| [TimeMachine: A Time Series is Worth 4 Mambas for Long-Term Forecasting](https://arxiv.org/abs/2403.09898) | 2024 | Multi-resolution Mamba | 4 parallel branches + MLP | ECAI | [Code](https://github.com/Atik-Ahamed/TimeMachine) |
| [Chimera: Effectively Modeling Multivariate Time Series with 2-Dimensional State Space Models](https://arxiv.org/abs/2406.04320) | 2024 | 2D joint-axis scan | Time x channel selective scan | NeurIPS | announced |

## Hybrid Architectures

Hybrid models combine Mamba with modules that compensate for weaknesses of pure selective scans: attention for content selection, MLP/EinFFT mixers for channel mixing, CNNs for local patterns, and decomposition or Fourier blocks for multi-frequency structure.

| Paper / Method | Year | Category | Hybrid Component | Venue / Source | Code |
| --- | --- | --- | --- | --- | --- |
| [Cross-Domain Time-Frequency Mamba: A More Effective Model for Long-Term Time Series Forecasting](https://doi.org/10.1016/j.knosys.2026.115341) | 2026 | Time-frequency hybrid | Coupled time/frequency Mamba scans | Knowledge-Based Systems | announced |
| [Attention Mamba: Time Series Modeling with Adaptive Pooling Acceleration and Receptive Field Enhancements](https://arxiv.org/abs/2504.02013) | 2025 | Attention hybrid | Adaptive pooling + attention + Mamba | IEEE Access | announced |
| [DIMformer: A Dynamic Inverted Transformer With Mamba-Cross-Variable Linear Attention for Multivariate Time Series Forecasting](https://doi.org/10.1109/ACCESS.2025.3645346) | 2025 | Attention hybrid | Mamba-cross-variable linear attention | IEEE Access | announced |
| [HyMaTE: A Hybrid Mamba and Transformer Model for EHR Representation Learning](https://doi.org/10.1145/3765612.3767245) | 2025 | Healthcare attention hybrid | Mamba temporal encoder + Transformer channel mixer | ACM BCB | [Code](https://github.com/healthylaife/HyMaTE) |
| [Affirm: Interactive Mamba with Adaptive Fourier Filters for Long-Term Time Series Forecasting](https://doi.org/10.1609/AAAI.V39I20.35463) | 2025 | Fourier hybrid | Adaptive Fourier filters | AAAI | [Code](https://github.com/congyutao0725/AFFIRM) |
| [KARMA: A Multilevel Decomposition Hybrid Mamba Framework for Multivariate Long-Term Time Series Forecasting](https://arxiv.org/abs/2506.08939) | 2025 | Decomposition hybrid | STL-style multilevel decomposition | arXiv | [Code](https://github.com/yedadasd/KARMA) |
| [CMDMamba: Dual-Layer Mamba Architecture with Dual Convolutional Feed-Forward Networks for Efficient Financial Time Series Forecasting](https://doi.org/10.3389/frai.2025.1599799) | 2025 | CNN hybrid | Depthwise and dilated convolutional FFNs | Frontiers in Artificial Intelligence | [Code](https://github.com/JadenZheng/CMDMamba) |
| [TimeMamba: A Mamba-Based Long-Term Time Series Forecasting Method with Fourier Analysis](https://arxiv.org/abs/2502.03430) | 2025 | Frequency/CNN hybrid | Fourier branch + Mamba | arXiv | announced |
| [Integration of Mamba and Transformer - MAT for Long-Short Range Time Series Forecasting with Application to Weather Dynamics](https://arxiv.org/abs/2409.08530) | 2024 | Attention hybrid | Mamba branch + Transformer branch | arXiv | [Code](https://github.com/mwxinnn/MAT) |
| [SST: Multi-Scale Hybrid Mamba-Transformer Experts for Time Series Forecasting](https://arxiv.org/abs/2404.14757) | 2024 | Mixture-of-experts attention hybrid | Mamba/Transformer experts + sparse gate | arXiv | [Code](https://github.com/XiongxiaoXu/SST) |
| [FMamba: Mamba Based on Fast-Attention for Multivariate Time-Series Forecasting](https://arxiv.org/abs/2407.14814) | 2024 | Fast-attention hybrid | Fast linear attention inside Mamba stack | arXiv | [Code](https://github.com/XieFanrong/FMamba) |
| [Can Mamba Learn How to Learn? A Comparative Study on In-Context Learning Tasks](https://arxiv.org/abs/2402.04248) / MambaFormer | 2024 | Mamba-Transformer interleaving | Alternating Mamba and Transformer blocks | arXiv | [Code](https://github.com/Alexia-Jolicoeur-Martineau/Mamba) |
| [SiMBA: Simplified Mamba-Based Architecture for Vision and Multivariate Time Series](https://arxiv.org/abs/2403.15360) | 2024 | EinFFT / MLP mixer hybrid | EinFFT channel mixer + Mamba time mixer | arXiv | [Code](https://github.com/badripatro/Simba) |
| [MambaMixer: Efficient Selective State Space Models with Dual Token and Channel Selection](https://arxiv.org/abs/2403.19888) | 2024 | MLP-Mixer style hybrid | Dual token/channel selective scans | arXiv | [Code](https://github.com/behrouzs/MambaMixer) |
| [UmambaTSF: A U-Shaped Multi-Scale Long-Term Time Series Forecasting Method Using Mamba](https://arxiv.org/abs/2410.11278) | 2024 | U-Net / CNN hybrid | U-shaped encoder-decoder with Mamba blocks | arXiv | [Code](https://github.com/lianghao228/UmambaTSF) |

## Specialized Designs

Specialized models are driven by an application domain or deployment constraint rather than by a generic backbone change. They often reuse methods from the previous branches but add domain structure, graph priors, cross-domain losses, federated aggregation, or foundation-model pretraining.

| Method | Year | Area | Backbone | Channel | Pretraining / Deployment | Code |
| --- | --- | --- | --- | --- | --- | --- |
| [BiG-Mamba](https://doi.org/10.1007/978-981-96-9946-9_26) | 2025 | Spatio-temporal | Bi-Mamba + graph | CC | - | announced |
| [Affirm](https://doi.org/10.1609/AAAI.V39I20.35463) | 2025 | Climate / weather | Mamba + FFT | CD | - | [Code](https://github.com/congyutao0725/AFFIRM) |
| [CMDMamba](https://doi.org/10.3389/frai.2025.1599799) | 2025 | Finance | Mamba + CNN | CD | - | [Code](https://github.com/JadenZheng/CMDMamba) |
| [HSTM](https://arxiv.org/abs/2503.11387) | 2025 | Finance / spatial | Spatial + temporal Mamba | CC | - | announced |
| [HyMaTE](https://doi.org/10.1145/3765612.3767245) | 2025 | Healthcare / EHR | Mamba + Transformer | CC | - | [Code](https://github.com/healthylaife/HyMaTE) |
| [FedRMamba](https://doi.org/10.1145/3774904.3792712) | 2025 | Federated forecasting | Mamba | CI | Federated residual updates | announced |
| [Chimera](https://arxiv.org/abs/2406.04320) | 2024 | Spatio-temporal | 2D Mamba | CD | - | announced |
| [MAT](https://arxiv.org/abs/2409.08530) | 2024 | Climate / weather | Mamba + attention | CD | - | [Code](https://github.com/mwxinnn/MAT) |
| [MambaStock](https://arxiv.org/abs/2402.18959) | 2024 | Finance | Pure Mamba | CI | - | [Code](https://github.com/zshicode/MambaStock) |
| [Graph-Mamba](https://arxiv.org/abs/2410.03707) | 2024 | Finance / graph | Bi-Mamba + GCN | CC | - | [Code](https://github.com/Ali-Meh619/SAMBA) |
| [DGMamba](https://arxiv.org/abs/2404.07794) | 2024 | Domain generalization | Mamba | CI | Domain-invariant loss | [Code](https://github.com/longshaocong/DGMamba) |
| [Mamba4Cast](https://arxiv.org/abs/2410.09385) | 2024 | Zero-shot forecasting | Mamba | CI | Synthetic pretraining; GIFT-Eval | [Code](https://github.com/automl/mamba4cast) |
| [SpaceTime](https://arxiv.org/abs/2303.09489) | 2023 | Foundation / pre-Mamba SSM | SSM | CI | Foundation-style SSM forecaster | [Code](https://github.com/HazyResearch/spacetime) |



## Performance Comparison

Reported MSE / MAE of Mamba time-series methods on the standard long-term multivariate forecasting benchmarks. Each cell averages the four MSE/MAE values the source paper reports at forecast horizons *H* ∈ {96, 192, 336, 720} (future steps predicted). The *L* column is the lookback length (past steps used as input) and is distinct from *H*: all rows average the same four *H*, but *L* differs across papers. The eight benchmarks are split across three sub-tables to keep the layout readable. **Italic** entries (e.g. `*0.469*`) are conducted by us — the source paper does not report that cell, and the value comes from our own runs. Plain entries are reported in the source paper. **Bold** marks the best value per column. `—` means the cell is not yet measured. Bottom-block rows are non-Mamba reference baselines (PatchTST, iTransformer, TimesNet, DLinear).

### Part 1 / 3: ETTh1, ETTh2, ETTm1

| Method | L | ETTh1 MSE | ETTh1 MAE | ETTh2 MSE | ETTh2 MAE | ETTm1 MSE | ETTm1 MAE |
| --- | --- | --- | --- | --- | --- | --- | --- |
| *Pure Selective-SSM Forecasters* | | | | | | | |
| S-Mamba | 96 | 0.455 | 0.448 | 0.381 | 0.405 | 0.398 | 0.405 |
| MambaTS | 720 | *0.469* | *0.460* | 0.339 | 0.381 | *0.435* | *0.427* |
| DTMamba | 96 | 0.444 | 0.435 | 0.363 | 0.395 | 0.388 | 0.398 |
| CMamba | 96 | 0.433 | 0.425 | 0.368 | 0.391 | 0.376 | 0.379 |
| CMMamba | 336 | **0.383** | 0.416 | 0.297 | **0.363** | 0.354 | 0.382 |
| SiMBA-TS | 96 | 0.446 | 0.432 | 0.361 | 0.391 | 0.383 | 0.396 |
| *Bidirectional / Multi-Directional Scans* | | | | | | | |
| Bi-Mamba+ | 96 | 0.437 | 0.431 | 0.372 | 0.399 | 0.378 | 0.396 |
| Chimera | 96 | 0.405 | 0.424 | **0.318** | 0.375 | 0.345 | **0.377** |
| *Hybrid Architectures* | | | | | | | |
| SiMBA | 96 | 0.394 | **0.405** | 0.336 | 0.378 | 0.419 | 0.420 |
| MambaMixer | 512 | 0.398 | *0.463* | **0.280** | *0.534* | **0.336** | *0.429* |
| Affirm | var | 0.411 | 0.423 | 0.331 | 0.381 | 0.344 | **0.377** |
| KARMA | 96 | 0.367† | 0.387† | 0.367† | 0.387† | 0.367† | 0.387† |
| SST | 672 | 0.393 | 0.421 | 0.333 | 0.381 | 0.347 | 0.386 |
| AttMamba | 96 | *0.469* | *0.471* | *0.576* | *0.525* | *0.434* | *0.434* |
| FMamba | 96 | *0.466* | *0.465* | *0.577* | *0.523* | *0.433* | *0.427* |
| MAT | 96 | *0.469* | *0.469* | *0.575* | *0.530* | *0.432* | *0.439* |
| *Reference non-Mamba baselines* | | | | | | | |
| PatchTST | 336 | 0.413 | 0.434 | 0.330 | 0.379 | 0.352 | 0.380 |
| iTransformer | 96 | 0.383† | 0.399† | 0.383† | 0.399† | 0.383† | 0.399† |
| TimesNet | 96 | 0.458 | 0.450 | 0.414 | 0.427 | 0.400 | 0.406 |
| DLinear | 336 | 0.456 | 0.452 | 0.559 | 0.515 | 0.403 | 0.407 |

`†` ETT-averaged value: the paper reports only a single average across the four ETT subsets, not per-subset numbers, so the same value is repeated across ETTh1, ETTh2, ETTm1 (and ETTm2 in Part 2 / 3 below).

### Part 2 / 3: ETTm2, Electricity (ECL), Weather

| Method | L | ETTm2 MSE | ETTm2 MAE | ECL MSE | ECL MAE | Weather MSE | Weather MAE |
| --- | --- | --- | --- | --- | --- | --- | --- |
| *Pure Selective-SSM Forecasters* | | | | | | | |
| S-Mamba | 96 | 0.288 | 0.332 | 0.170 | 0.265 | 0.251 | 0.276 |
| MambaTS | 720 | 0.247 | 0.310 | 0.155 | 0.251 | **0.219** | **0.257** |
| DTMamba | 96 | 0.278 | 0.323 | 0.196 | 0.285 | 0.258 | 0.279 |
| CMamba | 96 | 0.273 | 0.316 | 0.169 | 0.258 | 0.237 | 0.259 |
| CMMamba | 336 | 0.254 | 0.321 | *0.203* | *0.308* | 0.225 | 0.261 |
| SiMBA-TS | 96 | 0.281 | 0.327 | *0.204* | *0.305* | *0.275* | *0.321* |
| *Bidirectional / Multi-Directional Scans* | | | | | | | |
| Bi-Mamba+ | 96 | 0.281 | 0.328 | 0.166 | 0.263 | 0.243 | 0.272 |
| Chimera | 96 | 0.250 | 0.316 | **0.154** | **0.249** | **0.219** | 0.258 |
| *Hybrid Architectures* | | | | | | | |
| SiMBA | 96 | 0.287 | 0.341 | 0.186 | 0.275 | 0.254 | 0.284 |
| MambaMixer | 512 | 0.246 | *0.416* | 0.177 | *0.311* | 0.239 | *0.312* |
| Affirm | var | 0.252 | 0.315 | 0.157 | 0.250 | 0.226 | 0.261 |
| KARMA | 96 | 0.367† | 0.387† | 0.168 | 0.261 | 0.250 | 0.277 |
| SST | 672 | **0.234** | **0.296** | 0.170 | 0.267 | 0.227 | 0.262 |
| AttMamba | 96 | *0.370* | *0.419* | 0.167 | 0.262 | 0.247 | 0.276 |
| FMamba | 96 | *0.367* | *0.419* | 0.169 | 0.269 | 0.247 | 0.293 |
| MAT | 96 | *0.371* | *0.415* | *0.213* | *0.302* | 0.246 | 0.286 |
| *Reference non-Mamba baselines* | | | | | | | |
| PatchTST | 336 | 0.255 | 0.315 | 0.161 | 0.252 | 0.256 | 0.279 |
| iTransformer | 96 | 0.383† | 0.399† | 0.178 | 0.270 | 0.258 | 0.278 |
| TimesNet | 96 | 0.291 | 0.333 | 0.192 | 0.295 | 0.259 | 0.287 |
| DLinear | 336 | 0.350 | 0.401 | 0.166 | 0.264 | 0.248 | 0.300 |

### Part 3 / 3: Traffic, Solar-Energy

| Method | L | Traffic MSE | Traffic MAE | Solar MSE | Solar MAE |
| --- | --- | --- | --- | --- | --- |
| *Pure Selective-SSM Forecasters* | | | | | |
| S-Mamba | 96 | 0.414 | 0.276 | 0.240 | 0.273 |
| MambaTS | 720 | 0.373 | 0.262 | **0.184** | **0.247** |
| DTMamba | 96 | 0.507 | 0.326 | *0.255* | *0.290* |
| CMamba | 96 | 0.444 | 0.265 | *0.247* | *0.292* |
| CMMamba | 336 | *0.627* | *0.343* | *0.253* | *0.297* |
| SiMBA-TS | 96 | *0.635* | *0.348* | *0.262* | *0.285* |
| *Bidirectional / Multi-Directional Scans* | | | | | |
| Bi-Mamba+ | 96 | 0.404 | 0.272 | 0.227 | 0.255 |
| Chimera | 96 | 0.403 | 0.286 | *0.260* | *0.289* |
| *Hybrid Architectures* | | | | | |
| SiMBA | 96 | 0.493 | 0.291 | *0.248* | *0.286* |
| MambaMixer | 512 | 0.420 | *0.351* | *0.247* | *0.285* |
| Affirm | var | 0.392 | 0.268 | *0.249* | *0.295* |
| KARMA | 96 | 0.453 | 0.284 | *0.253* | *0.289* |
| SST | 672 | **0.350** | **0.250** | *0.255* | *0.291* |
| AttMamba | 96 | *0.631* | *0.358* | 0.235 | 0.278 |
| FMamba | 96 | *0.635* | *0.356* | 0.213 | 0.270 |
| MAT | 96 | *0.637* | *0.352* | *0.262* | *0.297* |
| *Reference non-Mamba baselines* | | | | | |
| PatchTST | 336 | 0.391 | 0.264 | *0.251* | *0.290* |
| iTransformer | 96 | 0.428 | 0.282 | 0.233 | 0.262 |
| TimesNet | 96 | 0.620 | 0.336 | *0.257* | *0.284* |
| DLinear | 336 | 0.434 | 0.295 | *0.253* | *0.287* |

**Best per column in bold.** Cross-row comparisons are only strictly meaningful within a fixed *L* (lookback). MambaTS, SST, MambaMixer, CMMamba, PatchTST, and DLinear use longer input windows (*L* ∈ {336, 512, 672, 720}) than the *L* = 96 default of most other Mamba methods; "var" means the lookback varies across datasets in the source paper.


## Datasets and Benchmarks

| Dataset / Benchmark | Domain | Length | Channels | Frequency | Used by examples |
| --- | --- | --- | --- | --- | --- |
| [ETTh1, ETTh2](https://github.com/zhouhaoyi/ETDataset) | Electricity | 17,420 | 7 | 1h | All systems |
| [ETTm1, ETTm2](https://github.com/zhouhaoyi/ETDataset) | Electricity | 69,680 | 7 | 15m | All systems |
| [Electricity](https://archive.ics.uci.edu/dataset/321/electricityloaddiagrams20112014) | Electricity | 26,304 | 321 | 1h | C-Mamba, CMamba, CMMamba, MambaMixer |
| [Traffic](https://pems.dot.ca.gov/) | Transportation | 17,544 | 862 | 1h | Chimera, S-Mamba, GCMNet, DIMformer |
| [Weather](https://www.bgc-jena.mpg.de/wetter/) | Climate | 52,696 | 21 | 10m | MAT, Affirm, KARMA, CDTF-Mamba |
| [Solar-Energy](https://github.com/laiguokun/multivariate-time-series-data) | Energy | 52,560 | 137 | 10m | S-Mamba, Bi-Mamba+, RLMamba |
| [ILI](https://www.cdc.gov/flu/weekly/) | Health | 966 | 7 | 1w | TimeMachine, MambaTS, Mamba+UQ |
| [PEMS04](https://github.com/guoshnBJTU/ASTGCN/tree/master/data) | Traffic | 16,992 | 307 | 5m | Chimera, HSTM, BiG-Mamba |
| [PEMS08](https://github.com/guoshnBJTU/ASTGCN/tree/master/data) | Traffic | 17,856 | 170 | 5m | Chimera, HSTM |
| [Exchange-Rate](https://github.com/laiguokun/multivariate-time-series-data) | Finance | 7,588 | 8 | 1d | MambaStock, MambaTS, CMDMamba |
| [Stock A-share](https://tushare.pro/) / [S&P 500](https://finance.yahoo.com/quote/%5EGSPC/history/) | Finance | varies | varies | 1d | MambaStock, CMDMamba, HSTM |
| [GIFT-Eval](https://github.com/SalesforceAIResearch/gift-eval) | Multi-domain | varies | varies | varies | Mamba4Cast |
| [Monash Forecasting Repository](https://forecastingdata.org/) | Multi-domain | varies | varies | varies | Mamba4Cast pretraining and evaluation |


## Evaluation Metrics

| Metric | Family | What it measures | Suitable use |
| --- | --- | --- | --- |
| MSE | Point forecast | Mean squared deviation over horizon and channels | Peak-sensitive energy, weather, and Gaussian-residual regimes |
| MAE | Point forecast | Mean absolute deviation | Robust comparison under heavy-tailed spikes |
| RMSE | Point forecast | MSE in original units | Human-readable absolute error scale |
| MAPE | Scale-free | Average relative error | Strictly positive non-zero targets across scales |
| SMAPE | Scale-free | Symmetric bounded relative error | Cross-series comparison when targets are small but not zero |
| MASE | Scale-free | MAE relative to naive or seasonal naive forecast | Monash-style cross-dataset skill aggregation |
| CRPS | Probabilistic | Calibration and sharpness of predictive CDF | Probabilistic forecasts such as Mamba+UQ |
| NLL | Probabilistic | Likelihood under predictive distribution | Explicit probabilistic decoders with trusted distribution family |
| Hit rate | Directional | Sign/direction accuracy | Finance, regime detection, and change-point tasks |
| Params / FLOPs | Efficiency | Model size and theoretical compute | Hardware-independent architecture comparison |
| Latency | Efficiency | Forward-pass wall time at fixed lookback and horizon | Deployment and long-context serving cost |


## Disclaimer

Feel free to contact us if you have any queries or exciting news on Mamba for time series. In addition, we welcome all researchers to contribute to this repository and further contribute to the knowledge of Mamba for time series fields. It would be great if contributions keep the repository aligned with the survey taxonomy

If you have some other related references, please feel free to create a Github issue with the paper information. We will glady update the repos according to your suggestions. (You can also create pull requests, but it might take some time for us to do the merge)

-----------
**Backup Statistics**

![Visitors](https://margherita-gustatory-zane.ngrok-free.dev/badge/tamlhp%2Fawesome-mamba-ts.svg?ngrok-skip-browser-warning=true)
