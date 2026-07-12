# CD-LAM — Project Page

Project page for **CD-LAM: Causally Debiased Latent Action Model for Embodied Action Conditioned World Models** — a research project by **Aether AI** and **UC San Diego**.

**Live page:** https://yufanwei.github.io/CD-LAM-project-page/ · **Code:** https://github.com/yufanwei/CD-LAM · **Model:** https://huggingface.co/yufanwei/CD-LAM · **Paper:** `static/paper/CD-LAM.pdf` (arXiv coming soon)

## About

CD-LAM is a LAM-side **causal debiasing** method for continuous latent actions.

Reconstruction-trained latent action models (LAMs) often encode action-irrelevant confounders — background motion, camera motion, object appearance — into their latent actions. Downstream action-conditioned world models (ACWMs) then receive these confounders as part of their action condition: rollouts remain visually plausible, but action following quietly fails (a zero action no longer freezes the embodiment; transferred actions fail to steer new scenes).

CD-LAM debiases the latent action space **before** world-model training, combining three objectives — **embodiment-centric reconstruction**, **action-centric contrastive learning**, and **latent space calibration** — in a lightweight three-stage pipeline (LAM debiased fine-tuning → ACWM debiased fine-tuning → robot action based training), while keeping the downstream action conditioning format unchanged.

**Highlights** (vs. DreamDojo, at 2B and 14B scale):

- **−42% / −26%** action-following error (FDCE) for latent-action conditioned rollouts
- **−35% / −30%** FDCE after robot action based training, with **+0.75 / +1.0 dB** PSNR
- Matches the baseline's full 50k-step budget with **3k / 6k** steps (**>12× fewer** updates); 1 hour of debiasing data already unlocks most of the gain

## Site structure

Single-file `index.html` (all CSS/JS inline); figures in `static/images/`; paper PDF in `static/paper/CD-LAM.pdf`.

The page embeds an interactive **rollout gallery** (`#gallery`) with three blocks — robot-action rollouts, zero-action intervention `do(u=0)`, and target-action transfer — each with a 2B/14B switch, synced side-by-side playback, and featured + "more" examples. It also includes an animated causal-graph figure, a live zero-action demo in the Problem section, an auto-looping highlight reel, and a hero background video wall.

- Videos: `static/videos/<group>/sNNN_{gt,ours,dream,donor}.mp4` (~55 MB total, lazy-loaded)
- Sample manifest (FDCE, episode ids, notes): inlined in `index.html`; source of truth in `static/videos/manifest.json`
- Montages (hero wall + highlight reel): `static/videos/montage/`
- Provenance / mapping back to eval export dirs: `static/videos/SELECTED.md`
- `transfer*/s288` donors are horizontally flipped (mirrored-arm episodes; noted on-page)
- A latent-action (Stage 2, EgoDex) gallery block is wired but hidden: it auto-appears once `latent2b`/`latent14b` groups (same export format) are added to the manifest and clips to `static/videos/latent{2b,14b}/`

Preview locally by opening `index.html` directly (the manifest is inlined, so `file://` works) or with `python3 -m http.server`.

## Citation

```bibtex
@article{wei2026cdlam,
  title   = {Causally Debiased Latent Action Model for Embodied Action Conditioned World Models},
  author  = {Wei, Yufan and Zhou, Kun and Mao, Lingjun and Zhang, Zijun and Xu, Ziming and Xi, Ziqiao and Liang, Shuang and Han, Ruobing and Yan, Yuchen and Wang, Xinyue and Feng, Fan and Huang, Biwei},
  journal = {Under review},
  year    = {2026}
}
```
