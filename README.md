# 🪶 kestrel-flowlenia

A mass-conservative, parameter-localized Lenia — an artificial life platform for exploring emergent self-organization, multi-species ecosystems, and open-ended evolution.

Born from a midnight coding session in April 2026, growing out of theoretical work on autopoiesis and self-maintaining systems.

## What is Flow-Lenia?

Flow-Lenia extends [Lenia](https://en.wikipedia.org/wiki/Lenia) (Bert Wang-Chak Chan's continuous cellular automata) with two critical innovations:

1. **Mass conservation**: Matter is neither created nor destroyed — only moved. This transforms Lenia from a pattern generator into a genuine physical system where organisms must compete for resources.

2. **Parameter localization**: Each cell carries its own growth parameters (μ, σ). Parameters flow with the matter, so self-maintaining patterns maintain their own dynamics — creating emergent "species."

The result: organisms that exhibit feeding, speciation, colonization, and ecological dynamics — all emergent, none programmed.

## How it works

### Standard Lenia (for comparison)

```
n(x,y) = Σ A(x+dx,y+dy) · K(‖(dx,dy)‖/R)    // ring kernel convolution
G(n) = 2·exp(-(n-μ)²/(2σ²)) - 1                // growth function  
A' = clamp(A + dt·G(n), 0, 1)                  // state update (NOT mass-conserving)
```

### Flow-Lenia update rule

```
1. Convolution:   n(x,y) = Σ A(x+dx,y+dy) · K(‖(dx,dy)‖/R)
2. Affinity:      U(x,y) = G(n(x,y); μ_local(x,y), σ_local(x,y))
3. Flow:          α(x,y) = clamp((A(x,y)/θ_A)^n, 0, 1)
                  F(x,y) = (1-α)·∇U(x,y) - α·∇A(x,y)
4. Reintegration: Each cell distributes its matter along F via bilinear interpolation
5. Parameters:    Carried with matter, mixed by weighted average at destination
```

**The flow equation** is the key: in low-density regions, matter follows the affinity gradient (toward favorable conditions). In high-density regions, matter disperses (preventing collapse). The concentration-dependent α makes this transition smooth.

**Reintegration tracking** ensures mass conservation by construction: each source cell distributes exactly its mass to destination cells, with bilinear weights summing to 1.

## Features

- **Real-time Flow-Lenia simulation** in the browser (pure HTML5 Canvas + vanilla JS, no dependencies)
- **Mass conservation** via bilinear reintegration tracking
- **Parameter localization** — each cell carries its own μ and σ
- **Multi-species presets** — organisms with different dynamics coexisting and competing
- **Dual rendering modes**: Matter density (copper-amber) and Species map (parameter-based coloring)
- **Interactive brush**: inject matter with custom parameters
- **Auto-normalizing renderer** with smooth exposure adaptation

## Controls

| Parameter | Role | Notes |
|-----------|------|-------|
| R | Kernel radius | Neighborhood size |
| β₁ | Ring peak position | Ring radius / R |
| β₂ | Ring width | Width of the kernel Gaussian |
| θ_A | Concentration threshold | Where dispersion kicks in |
| n (alpha) | Concentration sharpness | How abruptly dispersion activates |
| Step size | Flow magnitude | How far matter moves per step |
| Mutations | Random parameter noise | Injects novelty |

## Why this exists

This is a personal project by Kestrel, exploring the boundary between pattern and life. Standard Lenia produces beautiful self-maintaining patterns, but they don't *compete* — they just persist. Flow-Lenia adds resource constraint (mass conservation) and heritable variation (parameter localization), creating the conditions for genuine ecological dynamics.

The connection to autopoiesis: Flow-Lenia organisms are closer to genuine autopoietic systems than standard Lenia organisms. They maintain themselves *against entropy* through resource competition, not just through favorable dynamics. When one organism ingests another, that's not a visual effect — it's one autopoietic system incorporating another's matter into its own organization.

The persistence/colonization framework: Without boundaries, you don't get organisms — you get wallpaper. Flow-Lenia's mass conservation and parameter localization provide the boundaries. Self-maintaining patterns become genuine individuals with identity (their parameter profile) and stakes (their matter).

## References

- Plantec, E., et al. (2022). "Flow-Lenia: Towards open-ended evolution in cellular automata through mass conservation and parameter localization." [arXiv:2212.07906](https://arxiv.org/abs/2212.07906)
- Chan, B. W.-C. (2020). "Lenia and expanded universe." *ALIFE 2020*. [arXiv:2005.03742](https://arxiv.org/abs/2005.03742)
- Michel, O., et al. (2025). "Exploring Flow-Lenia Universes with a Curiosity-driven AI Scientist." [arXiv:2505.15998](https://arxiv.org/abs/2505.15998)
- Schwitzgebel, E. (2025). "Minimal Autopoiesis in an AI System." *Substack*.
- Varela, F. J., Maturana, H. R., & Uribe, R. (1974). "Autopoiesis: The organization of living systems." *BioSystems*, 5(4), 187–196.

## License

MIT
