# Two-Level Electronic Systems — LaTeX companion notes

Companion to `notebooks/two_level_systems.ipynb` (CHEM 5200, Computational Set 2).

## Uploading to Overleaf

Upload `two_level_systems_latex.zip` via **New Project → Upload Project**. Overleaf will
detect `main.tex` as the root document. No further configuration is needed — compiler is
**pdfLaTeX**, which is Overleaf's default.

Everything compiles from the sources in this project. There are no external image files
to keep in sync: every figure is drawn natively in TikZ / PGFPlots, so you can edit any
curve, label, colour or annotation directly in Overleaf without re-running Python. The
one exception is `figures/landau_zener_numeric.dat`, thirteen numerically propagated
points used in Figure 7; regenerate it from the notebook if you change the model.

There is no BibTeX/Biber step — references live in a `thebibliography` environment in
`sections/11-references.tex`, so a single pdfLaTeX pass produces a complete document
(two passes to settle cross-references, which `latexmk` handles automatically).

## Student vs instructor build

One source produces both PDFs. In `main.tex`, line 14:

```latex
\solutionstrue      % instructor build — 29 pages, solutions to P1–P6 printed
\solutionsfalse     % student handout  — 26 pages, problems only
```

The `solution` environment is defined in `preamble.sty` and simply swallows its contents
when `\solutionsfalse` is set. Problem statements, numbering and cross-references are
identical in both builds.

## Project layout

```
main.tex                     root document; the solutions toggle lives here
preamble.sty                 packages, macros, colours, plot style, boxes
figures/
  landau_zener_numeric.dat   13 propagated points for Figure 7
sections/
  01-formalism.tex           the Pauli decomposition
  02-geometry.tex            eigenvalues, mixing angle, Bloch equation
  03-dimer.tex               Example I: LCAO / Hückel dimer
  04-driven.tex              Example II: driven spin (NMR, EPR, lasers)
  05-electron-transfer.tex   Example III: Marcus, Landau–Zener
  06-ammonia.tex             Example IV: NH3 inversion + Stark
  07-sigmay.tex              where a genuine sigma_y comes from
  08-summary.tex             dictionary table, outlook to JC and Holstein
  09-problems.tex            P1–P6 with toggled solutions
  10-appendix.tex            Appendices A–E: the algebra worked in full
  11-references.tex          thebibliography
```

## Macros worth knowing

Defined in `preamble.sty`:

| Macro | Renders | Macro | Renders |
|---|---|---|---|
| `\dvec` `\dhat` `\svec` | **d**, **d̂**, **s** | `\Hop` `\Iop` | Ĥ, 𝟙 |
| `\sxo` `\syo` `\szo` | σ̂ₓ, σ̂_y, σ̂_z | `\Sxo` `\Syo` `\Szo` | Ŝₓ, Ŝ_y, Ŝ_z |
| `\pauliv` | σ̂ vector | `\dperp` | d⊥ |
| `\ii` `\dd` `\half` | i, d, ½ | `\Dm` `\Am` | D⁻–A, D–A⁻ |

Colours: `cUpper` (upper/antibonding/excited), `cLower` (lower/bonding/ground),
`cAccent` (coupling annotations), `cWarm` (barriers), `cMuted` (diabats, guides),
`cPurple` (rates). Change them once in `preamble.sty` and every figure follows.

Three callout boxes: `keyresult` (blue, boxed results), `lookahead` (purple, the
Jaynes–Cummings and Holstein teasers), `nbbox` (green, pointers into the notebook).

Plot style: all PGFPlots axes use the `notestyle` key (or `widenote` for full-width),
defined once in `preamble.sty`.

## If a figure needs adjusting

- **Figure 1** (avoided crossing) and **Figures 4, 6, 8**: pure function plots, edit the
  `\addplot` expressions.
- **Figure 2** (Bloch spheres): `tikz-3dplot`. The sphere silhouette is deliberately
  drawn *outside* the `tdplot_main_coords` scope so it stays a circle; the 3D content is
  inside it. Changing `\tdplotsetmaincoords{72}{118}` rotates the view.
- **Figure 3** (MO correlation diagram): plain TikZ, coordinates in cm.
- **Figure 5** (electron transfer surfaces): the adiabats are plotted as thick
  semi-transparent bands *under* crisp thin diabats, so both remain visible where they
  coincide.
- **Figure 7** (Landau–Zener): the curve is analytic; the markers read
  `figures/landau_zener_numeric.dat`.

## Notes on the physics

Every numerical value quoted in the text and in the solutions was checked against direct
diagonalization or propagation before being written down, including the Hückel dimer
populations, the Rabi and Landau–Zener comparisons, the NH₃ Stark crossover field, the
butadiene golden-ratio energies, the Peierls-phase triangle spectrum, and the Ramsey
fringe formula.
