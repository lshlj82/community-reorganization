# Kaleidoscopic community reorganization: interactive demo

An in-browser, interactive reproduction of the stochastic-block-model toy example (Fig. 5) from

> Wonhee Jeong, Daekyung Lee, Heetae Kim, and Sang Hoon Lee,
> **"Kaleidoscopic reorganization of network communities across different scales,"**
> *Physical Review E* **111**, 014312 (2025).
> [https://doi.org/10.1103/PhysRevE.111.014312](https://doi.org/10.1103/PhysRevE.111.014312)

The paper shows that increasing the modularity resolution parameter γ does not simply split communities into smaller ones. Splitting and merging happen at the same time, which can make the number of communities *drop* as γ grows. This demo lets you watch that happen.

## What the demo does

- Generates the Fig. 5 network: a 400-node core (A) and a 200-node core (B) joined with probability 0.1, plus 30 peripheral clusters of 20 nodes (10 attached to A, 20 attached to B), each peripheral node sending one edge to a random node of its core.
- Runs a from-scratch JavaScript implementation of the Louvain algorithm with the resolution parameter of Eq. (1), `Q = (1/M) Σ_g (L_g − γ K_g² / 4M)`.
- **Live view:** drag γ and see the coarse-grained network of building blocks with detected communities, as in Fig. 5(b)–(e).
- **Sweep:** averages over several network realizations and Louvain runs to plot
  - the number of communities n_c(γ), cf. Fig. 5(a);
  - the largest and second-largest community sizes, cf. Fig. 2(b);
  - a block-membership heatmap across γ, a reduced version of the Sankey diagram in Fig. 3.
- **Theory panel:** evaluates the merge thresholds `γ = 2M·I_gh / (K_g K_h)` from Eq. (5) on the generated network and reports whether a dip in n_c is expected (the paper's inequality (8)).
- **Adjustable model:** every SBM parameter can be changed; presets include the paper's setup, equal cores (no dip), and swapped peripheries.

## Running it

Everything is in a single self-contained file, `index.html`. No build step or server is needed:

- open `index.html` directly in a browser, or
- publish the repository with GitHub Pages (Settings → Pages → deploy from the `main` branch root).

The page loads two web fonts from Google Fonts and falls back to system fonts when offline.

## Notes on the model

- The paper says the connection probability "within small and large communities is set to 0.5 and 0.7." Here this is read as 0.5 inside peripheral clusters and 0.7 inside both cores. All values are editable in the page.
- With these parameters, Eq. (5) predicts that the 200-node core (the one with 20 peripheral clusters) re-absorbs its periphery after the cores split, because its total degree is much smaller. The simulation agrees. The paper's text attributes this to the 400-node core; its Fig. 5(d) appears consistent with the 200-node core.
- Results are averaged over fewer runs than in the paper (100 realizations × 100 runs) by default; increase the counts in the page for smoother curves.

## Credits

This interactive demo was created by Claude Opus 5.5 (Anthropic), based on the paper above. All scientific credit belongs to the paper's authors.
