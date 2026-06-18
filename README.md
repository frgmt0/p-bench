# Penumbra

**Measuring how a model behaves at the edge of its own competence.**

## Abstract

Penumbra is a contamination-proof, procedurally generated reasoning benchmark.
Every problem is a deterministic function of a secret seed: at evaluation time a
generator constructs the task, a guaranteed solution, and, for unsolvable
variants, a short impossibility proof. Because instances are created on demand and
never published, they cannot appear in any training corpus.

The benchmark targets the penumbra, the band of difficulty where a model is
neither reliably succeeding nor reliably failing. Instead of a single accuracy
figure, Penumbra reports a difficulty-calibrated ability, defined as the problem
difficulty at which a model's success rate falls to a coin flip, together with a
discrimination measure of whether a model can separate solvable problems from
provably impossible ones. Problems span eleven families that instantiate distinct
reasoning primitives, including symbolic rewriting, invariant detection, inductive
rule discovery, constraint satisfaction, adversarial game play, spatial packing,
flow routing, and bounded planning. Several families are framed against common
priors so that memorized heuristics mislead rather than assist.

Round R1 evaluated three models zero-shot on five hundred problems. Calibrated
ability and discrimination both ordered the models consistently with their scale,
while an anti-prior physics family compressed that ordering almost to nothing, a
result that serves as a warning for deployment on systems which violate textbook
assumptions. Full results, figures, and the round report are in `results/`.

## A note on partial open source

This repository is a public record that the project exists, together with its
methodology and measured results. The implementation is intentionally not
published.

The reason is structural. The value of Penumbra depends on its problem
distribution staying unseen. The generators are compact enough that releasing them
would let anyone mass-produce the same distribution and train directly against it,
which would erase the contamination resistance that is the entire purpose of the
benchmark. Here, publishing the code and operating a trustworthy benchmark are
mutually exclusive, so we keep the code private.

The generators, the evaluation harness, and the control plane therefore remain
closed. Independent evaluation, auditing, and reproduction are available through
direct collaboration with the authors. To run a model against a sealed round, or
to verify a reported result, please reach out.

## Roadmap to full openness

The closed status of R1 is a temporary condition, not the end state. The intent is
always to open the methodology and the exact problems of each round, once doing so
can no longer compromise the measurement.

The trigger is saturation. A round retains value only while it still separates
models. Once frontier models saturate a round, that round stops discriminating and
has nothing left to protect, so it can be released in full. Releases follow that
schedule. When R3 is the active round, R1 will be published in its entirety,
including its exact puzzles, because by then it no longer provides any measurement
value. Each earlier round is opened as a later one renders it obsolete.

This places a standing obligation on the maintainer to keep developing p-bench so
that it consistently finds the edge, advancing the difficulty and the families
quickly enough to stay ahead of the models it measures. When p-bench as a whole has
served its purpose and can no longer be kept ahead of the frontier, the entire
project, generators included, will be open sourced.
