# The Covering Number $C(61,11,2)$ Is $39$

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24550537.svg)](https://doi.org/10.5281/zenodo.24550537)

**Paper, Pure Lean 4 Formalization, and Standalone Integer Certificates**

> **Author:** Zhiyu Xiong (University of Science and Technology of China)  
> **Paper:** [`C61-11-2-paper.pdf`](C61-11-2-paper.pdf) ([LaTeX source](C61-11-2-paper.tex))

---

## Main Results

1. **Exact Covering Number $C(61,11,2) = 39$ (Theorem 1.2):**  
   We prove that no $38$ blocks of size $11$ can cover all $\binom{61}{2} = 1830$ pairs of a $61$-element set. Combined with the explicit $39$-block covering design in [`Meliwat/covering-hunt`](https://github.com/Meliwat/covering-hunt/blob/master/records/C61_11_2_b39.txt) (committed October 17, 2026; an independent $39$-block upper bound by Hossein Farahani is also recorded on [The Covering Repository](https://coveringrepository.com), October 23, 2026), this settles $C(61,11,2) = 39$ (previously $37 \le C(61,11,2) \le 39$).

2. **Cascading Higher-Strength Lower Bounds (Corollary 1.3):**  
   By the Schönheim recursion $C(v,k,t) \ge \lceil \frac{v}{k} C(v-1,k-1,t-1) \rceil$:
   - $C(62,12,3) \ge \mathbf{202}$ (previous best tabulated lower bound: $192$, **+10**)
   - $C(63,13,4) \ge \mathbf{979}$ (previous best tabulated lower bound: $931$, **+48**)

3. **A Max-Cut Improvement to Horsley's Covering Bound (Theorem 1.1 & Corollary 1.2):**  
   Replacing the Caro–Tuza greedy $m$-independent set bound in Horsley's generalization of Fisher's inequality (2017) with a maximum $2$-cut bipartition of the excess multigraph gives the closed-form lower bound
   $$C(v,k,2) \ge \left\lceil \frac{v(r+2)}{k+2} \right\rceil \qquad \bigl(v = r(k-1) + 1,\; r < k \le 2r\bigr).$$
   This ten-line proof improves **$13$ tabulated lower bounds** in the frozen March 2026 La Jolla Covering Repository (and all $11$ corresponding entries in the November 26, 2026 snapshot of The Covering Repository), including $C(61,11,2) \ge 38$, and combines with public $27$-block constructions ([`Meliwat/covering-hunt`](https://github.com/Meliwat/covering-hunt/blob/master/records/C41_9_2_b27.txt) and [Arhan Canli / Quantavane](https://quantavane.com/results/coverings/c-41-9-2/), October 23, 2026) to settle a second exact value:
   - **$C(41,9,2) = 27$**

---

## Summary of Improved Lower Bounds (Theorem 1.1)

| $(v,k,2)$ | $r$ | Schönheim | Horsley (2017) | New LB | Best UB | Status |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| $(36,8,2)$ | 5 | 23 | 25 | **26** | 27 | $26 \le C \le 27$ |
| **$(41,9,2)$** | 5 | 23 | 26 | **27** | **27** | **$C = 27$ (Exact)** |
| $(46,10,2)$ | 5 | 23 | 26 | **27** | 28 | $27 \le C \le 28$ |
| $(55,10,2)$ | 6 | 33 | 36 | **37** | 39 | $37 \le C \le 39$ |
| **$(61,11,2)$** | 6 | 34 | 37 | **38** ($\to$ **39**) | **39** | **$C = 39$ (Exact)** |
| $(71,11,2)$ | 7 | 46 | 49 | **50** | 52 | $50 \le C \le 52$ |
| $(81,11,2)$ | 8 | 59 | 62 | **63** | 66 | $63 \le C \le 66$ |
| $(67,12,2)$ | 6 | 34 | 38 | **39** | 40 | $39 \le C \le 40$ |
| $(78,12,2)$ | 7 | 46 | 50 | **51** | 53 | $51 \le C \le 53$ |
| $(89,12,2)$ | 8 | 60 | 63 | **64** | 67 | $64 \le C \le 67$ |
| $(85,13,2)$ | 7 | 46 | 50 | **51** | 53 | $51 \le C \le 53$ |
| $(97,13,2)$ | 8 | 60 | 64 | **65** | 68 | $65 \le C \le 68$ |
| $(92,14,2)$ | 7 | 46 | 51 | **52** | 53 | $52 \le C \le 53$ |

---

## Repository Contents

| File | Description |
|---|---|
| `C61-11-2-paper.pdf` | Compiled 16-page English paper |
| `C61-11-2-paper.tex` | Full LaTeX source |
| `C61-11-2-proof.md` | Detailed Chinese technical proof notes aligned with the verification package |
| `C61-11-2-audit.txt` | Raw `#print axioms` audit output for all 285 Lean 4 declarations |
| `C61-11-2-replay.txt` | Isolated standard-library Python integer replay log |
| `C61-11-2-reviewed.zip` | Complete reproducible archive (711 files: `lean/`, `integer/`, `computational/`, `logs/`, `SHA256SUMS.txt`) |

**Archive SHA-256 (`C61-11-2-reviewed.zip`):**
```text
78e7daf13f9a0dd844090af1eedf839a9f3c7551fbdbf2b4ab08061cce122d58
```

---

## Verification Architecture & Reproducibility

The proof of $C(61,11,2) = 39$ is verified in two cleanly separated layers:

### 1. Pure Lean 4.36.0 Kernel (`lean/`, 240 `.lean` files, Mathlib v4.36.0)
- **Zero cheat keywords:** 0 occurrences of `sorry`, `admit`, `axiom`, `unsafe`, `implemented_by`, `extern`, `partial`, or `native_decide` across all 240 Lean source files.
- **Pure standard axioms only:** All 285 audited theorems in `C61-11-2-audit.txt` depend solely on `[propext, Classical.choice, Quot.sound]`.
- **Formalized scope:** Explicit 39-block upper bound (`Cover61.exists39`), full structural reduction ($t_j \le 4$, $9 \le a \le 12$, 5 degree profiles, all 567 local 4-low-point histograms, order-5 Latin squares), exhaustive classification of all 215 low-point skeletons (`Cover61.cover_catalogue`), purely combinatorial exclusion of the affine plane $\mathrm{AG}(2,3)$ (`Cover61.Affine.excluded`), kernel elimination of 170 of the 215 skeletons—proving any hypothetical 38-block cover must realize one of 45 specified skeletons (`Cover61.cover_remaining`)—containment of any surviving compatible support in the given conflict graph of `9-37.0` inside 121 representatives (`Cover61.Supports.Nine37.exhaustive`), and mathematical soundness of every integer certificate primitive.

To rebuild and audit Lean locally (after unzipping `C61-11-2-reviewed.zip`):
```bash
cd lean
lake exe cache get
lake build -j 1
lake env lean Audit.lean
```

### 2. Isolated Standard-Library Python Integer Replay (`integer/verify_all.py`)
- Uses **only Python 3.10+ standard library** (`-I -B -S` isolated mode), arbitrary-precision integer arithmetic, and **no external LP solver**.
- Matches all 215 Lean skeleton tables index-for-index against the certificate inputs, verifies all 1830 pairs of the 39-block design, checks computational exclusions for **250** degree-profile instances (610 strict integer Farkas contradictions, 886,299 replayable proof-tree nodes, 3,351 explicit isomorphisms, and 142 residual-block integer prices), and reconciles the full 251-instance ledger by referencing the separate Lean theorem for the affine-plane instance `9-49.0`.

To run the isolated replay (from the unzipped archive root):
```bash
python -I -B -S integer/verify_all.py
```

---

## Citation

```bibtex
@misc{Xiong2026C61,
  author       = {Zhiyu Xiong},
  title        = {The Covering Number $C(61,11,2)$ Is $39$, with a Max-Cut Improvement to Horsley's Covering Bound},
  year         = {2026},
  month        = nov,
  howpublished = {\url{https://github.com/XtraSensei/covering-61-11-2}}
}
```
