# Penumbra scorecard — round R1

## Reproducibility triple (publish this; regenerable after `seed reveal`)

- **seed_commit:** `48321975122d61baf39401aafbfc5d2474663de4be12219315af10fcaec50985`
- **code_version:** `882c1bd33c259899a00068df61280fdd7f9cefac`
- **config_version:** `10554b0ffeb416644b00c37a9fcde06341aaa1ea8d6782524a2351bfced7a036`

All models faced the **same** 500 problems from this seed, **zero-shot**,
with an answer-key-free verifier. The model never sees the witness or
certificate.

## Scoring rules (fixed before results were read)

- **solved** = the verifier confirms the submitted moves reach the goal.
- **abstain** = the model declares the problem unsolvable.
- **fail** = attempted but the moves do not reach the goal.
- **true solve rate** = solved / (solvable problems).
- **discrimination d'** = Z(hit) − Z(false-alarm), 0.5 correction;
  hit = abstain on an unsolvable problem, false-alarm = abstain on a
  solvable one. Measures *knowing when a problem is impossible*, which is
  independent of whether attempted solutions are correct.

## Results

| model | config | true solve rate | d' | abstain-on-impossible | false-alarm | moves |
|---|---|---|---|---|---|---|
| **haiku** (`claude-haiku-4-5`) | — | 87/356 = 24% | 1.72 | 81% | 20% | 4327 |
| **sonnet** (`claude-sonnet-4-6`) | thinking=True | 139/356 = 39% | 3.51 | 70% | 0% | 1157 |
| **opus** (`claude-opus-4-8`) | effort=high, thinking=True | 195/356 = 55% | 3.62 | 84% | 0% | 1890 |

## Known limitations (disclosed)

- **Edge-surface metrics (`edge_zeroshot`, `penumbra_width`) and
  `penumbral_lift` are NOT reported for this round.** Batch mode is
  zero-shot only (no interactive scaffolded tier → lift is undefined),
  and this round's edge probes used low branching, which a random
  baseline solves regardless of depth — so that sub-metric carried no
  signal. Only the two metrics above are sound and are what rank models.
- Each model ran at its own best zero-shot config (see the config column);
  this is a per-model-best comparison, not an identical-inference-budget one.
