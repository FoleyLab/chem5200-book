# Style Audit: Computational Set Notebooks

Audit of the five notebooks in `notebooks/`: `spin_one_half.ipynb`, `newton_raphson.ipynb`,
`two_qubit_entangled_DR.ipynb`, `vibronic_spectra_MgH_1.ipynb`, and `Basis_Sets_student.ipynb`.

Findings only — no edits were made to the notebooks as part of this audit. Reference
notebooks for style, per discussion, are `spin_one_half.ipynb` and `newton_raphson.ipynb`.
The Design Recipe audit excludes `Basis_Sets_student.ipynb` (not a Design Recipe notebook).

---

## 1. Design Recipe consistency

*(spin_one_half, newton_raphson, two_qubit_entangled_DR, vibronic_spectra_MgH_1)*

### Heading conventions (three different patterns in use)

- **newton_raphson** and **two_qubit_entangled_DR**: consistently use
  `### 🧩 Design Recipe: \`func_name\` — description`.
- **spin_one_half**: mixes `🧪`, `🧩`, and plain `🚧 Your Task` headings for the same kind of
  callout — no single pattern is used throughout.
- **vibronic_spectra_MgH_1**: uses a fourth pattern, `🧩 Function N — \`func_name\` (Design
  Recipe)`, numbering functions sequentially (Function 1 … Function 7) — none of the other
  notebooks number functions this way.

### Depth of scaffolding

- **spin_one_half** and **two_qubit_entangled_DR** spell out the full numbered 1–6 Design
  Recipe steps (Header/Purpose/Examples/Body/Test/Debug-Iterate) with guiding questions,
  every time a new function is introduced.
- **newton_raphson** deliberately compresses this after the first function into a one-line
  reminder plus the relevant equation, with an explicit stated rationale ("Since you've
  already practiced this recipe in Computational Set 1, we won't re-list all six steps...").
- **vibronic_spectra_MgH_1** uses bolded inline run-in labels (**Header.** **Purpose.**
  **Examples.** **Body / Test / Debug.**) rather than a numbered list — a fourth distinct
  presentation style.

### Code-blanking convention

- **spin_one_half**, **newton_raphson**, **two_qubit_entangled_DR**: blanks are marked with
  bare `...` and/or `# TODO:` comments.
- **vibronic_spectra_MgH_1**: uses a `# --- Body (students complete this) ---` banner to
  delimit the region a student would blank out — a different mechanism not used elsewhere.
  (This notebook is already the instructor-complete version; the banner is how the student
  version would be derived from it.)

### Shared strengths worth preserving

- **spin_one_half** and **two_qubit_entangled_DR** both include a "🔀 From Building Functions
  to Using Them" transition cell once Design Recipe scaffolding fades, explicitly naming all
  the functions built so far. **newton_raphson** and **vibronic** don't have an equivalent,
  though both keep introducing new recipe functions throughout, so the transition is less
  necessary structurally.

---

## 2. General style consistency

*(all five notebooks)*

### Header / title block

| Notebook | Colab link | Author byline | Learning outcomes heading | Summary section |
|---|---|---|---|---|
| spin_one_half | ✅ | ✅ (with link) | `#### Learning Outcomes` | ✅ `#### Summary` |
| newton_raphson | ✅ | ✅ (with link) | `#### Learning Outcomes` | ✅ `#### Summary` |
| two_qubit_entangled_DR | ❌ missing | ✅ + extra bio/project bullets | moved into first content section, not under title | ❌ none |
| vibronic_spectra_MgH_1 | ❌ missing | ❌ none | bold run-in text, not a heading | ❌ none (has "note on Design Recipe" + instructor note instead) |
| Basis_Sets_student | ✅ | ❌ none under title (legacy `__authors__`/`__credits__` code cell instead) | plain text, not styled as a heading | ❌ none |

`spin_one_half` and `newton_raphson` are near-identical in structure and are the strongest
reference points. `Basis_Sets_student` is the furthest from that pattern, consistent with it
being the most dated notebook of the five.

### Voice in learning outcomes

- **spin_one_half**, **newton_raphson**, and (perhaps surprisingly) **Basis_Sets_student**
  all use third person: "By the end of this workbook, **students** should be able to..."
- **two_qubit_entangled_DR** and **vibronic_spectra_MgH_1** switch to second person: "By the
  end of this **notebook/step, you** will/should be able to..."

### Emoji density

Ranges widely across the set:

- **Basis_Sets_student** — essentially none; plain academic prose throughout.
- **vibronic_spectra_MgH_1** and **newton_raphson** — most disciplined/purposeful.
  newton_raphson reserves 🧩 exclusively for Design Recipe headers and 📝 exclusively for
  "a note on..." asides, so the emoji carries real signal.
- **spin_one_half** and **two_qubit_entangled_DR** — heaviest and least systematic use.
  two_qubit in particular reuses 🧩 for section headers unrelated to the Design Recipe (e.g.
  "🧩 Step 1: Defining the Hamiltonian"), which dilutes 🧩 as a reliable visual marker.

### Hints and worked solutions

- **spin_one_half** and **newton_raphson** share a `<details><summary>💡 Solution</summary>`
  collapsible block for practice problems — solutions revealed after the student attempts
  the problem.
- **two_qubit_entangled_DR** has a superficially similar `<details>` block, but labels it
  "Hint" (not "Solution") and offers it pre-emptively rather than as a worked answer —
  same mechanism, different intent and label.
- **vibronic_spectra_MgH_1** has none (it's the answer key, not a scaffolded notebook).
- **Basis_Sets_student** has no scaffolding at all: no TODOs, no starter code, no hints, no
  asserts/tests — just numbered prose instructions and a bare "RESPONSE:" marker per part.

---

## 3. Bugs found (not style, but worth flagging)

Found incidentally while building the instructor solutions; fixed in the solution key but
still present in the student notebook as shipped.

- **`two_qubit_entangled_DR.ipynb`**, cell defining `commutator` tests: contains the literal,
  syntactically invalid line `assert ... complete with second example # = -sigma_z`. Running
  this cell as-is raises a `SyntaxError`.
- **`two_qubit_entangled_DR.ipynb`**, cell testing `density_matrix`: calls a misspelled
  `denistry_matrix(...)` and has the same invalid `assert ... complete with second example`
  placeholder line as above.
- **`two_qubit_entangled_DR.ipynb`**, time-evolution loop: with the given parameters
  (`n_time=800`, but `n_time_1 + n_time_2 ≈ 471`), the `if/elif` branch that picks `H1`/`H2`
  has no `else`, so once `i` exceeds `n_time_1 + n_time_2`, `rho_new` is never reassigned and
  the loop silently reuses the prior iteration's value for all remaining steps. Not a crash,
  but the population plot goes flat after `T2` in a way that's likely unintended.
- **`instructor_solutions/newton_raphson_v2_solved.ipynb`**: a leftover, stale solution file
  that doesn't match the current student notebook (different cell order/content, and its
  title still reads "Computational Set 13"). It has now been superseded by the freshly
  rebuilt `newton_raphson_solution.ipynb`, but the stale file itself hasn't been deleted —
  flag for cleanup.

---

## 4. Suggested next steps (not yet actioned)

1. Standardize on newton_raphson's `🧩 Design Recipe: \`func_name\`` heading pattern across
   spin_one_half, two_qubit_entangled_DR, and vibronic_spectra_MgH_1.
2. Decide on one code-blanking convention (bare `...`/TODO vs. banner comments) and apply it
   uniformly — this also determines how a student version of vibronic would be generated.
3. Bring two_qubit_entangled_DR and vibronic_spectra_MgH_1's header blocks in line with the
   spin_one_half/newton_raphson template (Colab link, author-with-link, `#### Learning
   Outcomes`, `#### Summary`), and give Basis_Sets_student the same treatment last, given how
   far it currently is from that template.
4. Settle on a single second- vs. third-person voice for learning outcomes.
5. Fix the two_qubit_entangled_DR bugs listed above.
6. Confirm whether `newton_raphson_v2_solved.ipynb` should be removed from
   `instructor_solutions/`.
