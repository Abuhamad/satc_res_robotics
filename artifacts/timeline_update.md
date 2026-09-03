# VLA Timeline Figure Update (fig:vla-timeline)

Scope: models to ADD to extend the timeline beyond its early-2025 horizon. All nodes below use bib keys already verified in `refs_v2_additions.bib`.

## 1. Final ordered list of NEW model nodes (earliest → latest)

| Order | Display name | \cite key | Approx. release (placement) |
|-------|--------------|-----------|------------------------------|
| 1 | OpenVLA-OFT | `openvla_oft` | Feb 2025 (arXiv) / RSS Jun 2025 — Q1–Q2 2025 |
| 2 | GR00T N1 | `gr00tn1` | Mar 2025 (Q1, arXiv 2503.14734) |
| 3 | Gemini Robotics | `geminirobotics2025` | Mar 2025 (Q1, arXiv 2503.20020) |
| 4 | Pi-0.5 | `pi05_2025` | Apr 2025 (Q2, arXiv) / CoRL Sep 2025 |

Note on horizon: the four verified models land in **Q1–Q2 2025**, not 2025 H2–2026. They are still strictly newer than the current rightmost 2025 nodes and correctly extend the figure, but no *verified* 2026-dated model reference currently exists in the bib.

## 2. Duplication check

- **RDT-1B (`rdt1b`) — EXCLUDED as a duplicate** of the existing `liu2024rdt` node already in the figure.
- `openvla_oft` (OpenVLA-OFT) is distinct from the existing OpenVLA node — OK to add.
- `pi05_2025` (Pi-0.5) is distinct from the existing Pi-0 (`black2024pi_0`) node — OK to add.
- GR00T N1 and Gemini Robotics are not present anywhere in the figure — OK to add.
- `badvla` / `advvla` are security/attack papers, not generalist models — correctly excluded.

## 3. Optional additions (NO verified bib entry — add only if user supplies/verifies a reference)

Do NOT invent bib keys for these. Approximate dates given only for eventual placement.

| Display name | Approx. release | Status |
|--------------|-----------------|--------|
| SpatialVLA | Jan 2025 | no verified bib key |
| SmolVLA | May–Jun 2025 | no verified bib key |
| WorldVLA | Jun 2025 | no verified bib key |
| MolmoAct | Aug 2025 | no verified bib key |
| GR-2 | 2024–2025 | no verified bib key |

## 4. Recommendation

Extend the existing 2025 row — the verified additions are all Q1–Q2 2025, so a new 2026 tier/row is **not** warranted until a verified 2026-dated model reference is available.
