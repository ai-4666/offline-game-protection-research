# Existing Offline Protection Techniques: Preliminary Results

2026-10-28 · Public research record. Internal implementation code and binaries remain private.

## Question and scope

This study examines established code-protection techniques through REA reconstruction, execution costs, and development observations. The specimen is one C game-state transition function, not a playable game or commercial protection product. The data-encoding and function-splitting variants are manual examples of the referenced technique families; they are not Tigress-generated outputs.

## Comparison

| Technique | Median per call | Relative to baseline | REA and reconstruction observation |
| --- | ---: | ---: | --- |
| Unprotected | 6.295 ns | 1.00× | Calculation decompiled; reconstruction matched. |
| Simple control-flow sample | 6.100 ns | 0.97× | Core calculation exposed; no separate reconstruction trial. |
| Function splitting | 7.448 ns | 1.18× | Individual calculations traceable; reconstruction matched. |
| Data encoding | 14.128 ns | 2.24× | Encoding, decoding, and core calculation traceable; reconstruction matched. |
| Simple VM | 126.518 ns | 20.10× | Interpreter and instruction data readable; reconstruction matched. |

![Microbenchmark results](figures/research-performance.png)

Dots show nine run measurements; red marks show medians. The horizontal axis is logarithmic. Each run made ten million calls, with nine randomly ordered runs per variant on WSL2 x86-64 and GCC 15.2.0 `-O2`. Final checksums agreed. This measures a single function, not frames, loading, or whole-game CPU/memory use. The VM function's visibility changed for separate linking, so its benchmark machine code need not exactly match the distributed executable.

All five variants agreed on 1,004 boundary and random inputs. Reconstructions of the unprotected, split, encoded, and VM versions matched their executables on another 302 inputs. **The investigator already knew the original source, so this was not a blind trial.** Reconstruction time and cost were not recorded. Finite agreement does not prove full equivalence or permit a statistical comparison of protection strength. Some function-argument information in REA pseudocode was incomplete.

## Developer and player impact

Manual source edits and individual compilations do not represent integration costs in a real engine. Single compile observations were 68.8 ms for unprotected code, 65.4 ms for control flow, 78.2 ms for splitting, 65.1 ms for encoding, and 76.4 ms for the VM. One measurement per variant cannot establish a meaningful difference. Source-edit effort, build pipelines, debugging, and update compatibility were not measured.

Execution-time differences were observed, but normal-game frame time, loading, saving, crashes, accessibility, and mod compatibility were not tested. These results do not establish an absence of player impact.

## Interpretation and next steps

These simple splitting, encoding, and VM implementations did not prevent REA-assisted reconstruction by a source-aware investigator. The control-flow sample exposed the original calculation, apparently after compiler simplification; optimization passes were not examined. This is an observation about these implementations, not a verdict on entire technique families.

Further work requires actual research tools and configurations, repeated evaluations without source access under equal budgets, and player/developer measurements in a real game build.

## References

- [Tigress transformation catalog](https://tigress.wtf/transformations.html): virtualization, splitting, encoding, and other technique families.
- [Tigress function splitting](https://tigress.wtf/split.html).
- [Tigress data encoding](https://tigress.wtf/encodeData.html).
- [Tigress downloads and terms](https://tigress.wtf/download.html): commercial use has separate licensing conditions. Tigress was not installed or executed in this study.
- [Obfuscation evaluation framework](https://www.mdpi.com/2076-3417/14/12/5056): separate treatment of analysis resistance and execution costs.
