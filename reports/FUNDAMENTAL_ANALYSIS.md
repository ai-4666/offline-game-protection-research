# Foundations of Offline Game Reconstruction Resistance

2026-10-28 · Public research record. Experimental code and executables remain private.

## Three different problems

1. Copying and reusing original files, assets, or protected modules.
2. Inspecting a binary or observing runtime state to reconstruct equivalent code.
3. Observing gameplay and input-output behavior to build a similar game.

These problems require different evaluations. Evidence that code is harder to inspect does not establish resistance to behavior-based reimplementation. An offline game runs on the user's machine, where the attacker may observe its code, data, execution, or outputs. Complex behavior may be difficult to learn completely from finite observations, but that possibility is not a security guarantee. A platform with a separate hardware trust boundary requires a separately defined threat model.

## Theory and its limits

Barak and colleagues showed that general-purpose virtual black-box obfuscation, under a specific formal definition, cannot apply to every program. Their result does not prove that every game is easy to analyze, that all obfuscation is useless, or that gameplay-based copying is always possible. See the [original paper](https://www.cs.ucla.edu/~sahai/work/web/2001%20Publications/Crypto_Barak2001.pdf) and the [author's explanation](https://www.boazbarak.org/papers/obf_informal).

A protection claim must specify what the attacker receives, what counts as success, and the available time and hardware. Artifacts include executables, extracted modules, and observable inputs and screens. Success might mean equivalent functionality, a similar game experience, or direct reuse of code and assets. A claim that only the analyst incurs costs, with exactly zero gameplay or development overhead, requires its own evidence.

## Preliminary input-output experiment

A separate test collected only the transformed sample's inputs and outputs. The investigator already knew the output-field layout and a small family of candidate formulas. After 30 random queries and 21 selected queries, one formula remained within that family. It matched another 300 inputs containing 32-bit integers.

This was a restricted attack on a small artificial sample with substantial prior knowledge. It does not show that a general game can be reconstructed in 51 observations. It does show that this sample's outputs carried useful information independently of binary obfuscation.

## Experimental direction

- Evaluate static-only analysis, dynamic observation, input-output-only access, and module copying separately.
- Compare reconstruction outcomes under stated input and time budgets, including long state histories and held-out inputs.
- Check baseline/transformed behavior and save/restart behavior, then measure actual engine frame time, memory, platform compatibility, and developer build/debug effort.
- Test whether a module or recovered behavior from one build can be reused against another. Different binary hashes alone do not establish an advantage from diversification.
- Treat hardware or an online trusted service as a change to the offline assumptions and player requirements that needs its own evaluation.

The table, VM, and diversification prototypes have not achieved general offline copy-impossibility. Future hypotheses should follow from the attacker's observations and resources and the game elements that need protection.
