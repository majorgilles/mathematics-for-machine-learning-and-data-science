# AGENTS.md

## Purpose

This repository contains follow-along mathematics notebooks for the DeepLearning.AI Mathematics for Machine Learning and Data Science Specialization. Treat notebooks as teaching material, not scratchpads: they should be mathematically careful, readable from top to bottom, and reproducible with the repository environment.

## Transcript-derived notebooks

- Preserve the lecture's order, examples, terminology, and conclusions.
- Convert spoken repetition and filler into concise prose; do not paste timestamps or an unedited transcript unless the task explicitly requests a verbatim archive.
- Separate what the source **states** from added explanation. Label added examples, inferred values, or synthetic data clearly.
- Never invent values that were visible in a lecture slide but absent from the supplied transcript. Explain the omission or use explicitly labeled illustrative data.
- Use one `## Video ...` section per lecture and focused `###` subsections for its ideas.
- End substantial sections with a short interpretation, checkpoint, or takeaway rather than only code output.

## Notebook narrative structure

A typical teaching notebook should use this order:

1. A single `#` title and a short statement of scope.
2. Learning objectives or a concept map.
3. Intuition and definitions before formal manipulation.
4. Equations with every symbol defined.
5. A small worked example.
6. Code or a visualization that verifies the mathematics.
7. A concise summary and optional self-check questions.

Keep each cell focused on one idea. Introduce a code cell with Markdown that tells the learner what to inspect, and explain the result after the cell when the interpretation is not obvious.

## Mathematical writing

Use LaTeX in Markdown for mathematical notation.

- Inline mathematics: `$f(x)$`, `$\theta$`, `$\frac{dy}{dx}$`.
- Display mathematics: `$$ ... $$` for important equations or derivations.
- Prefer conventional notation over plain-text approximations.
- Define symbols, domains, dimensions, and units at first use.
- Distinguish exact equality (`=`), definition (`:=` when useful), and approximation (`\approx`).
- State assumptions needed by a result, such as differentiability, nonzero denominators, or positive logarithm arguments.
- Show enough intermediate algebra that a learner can reproduce a derivation; do not jump from premise to result without explanation.
- Check formulas numerically when a short computation can expose sign, scaling, or indexing errors.

For optimization, distinguish clearly among a model, its parameters, a per-example loss, and an aggregate cost/objective. For multivariable objects, state shapes explicitly when they matter.

## Visualizations

- Every plot must have a descriptive title and labeled axes, including units when available.
- Add a legend when multiple data series, models, or regions appear.
- Use readable colors and markers; do not rely on color alone when a marker or line style can help.
- Keep plots deterministic. Set a random seed for generated data and label generated data as synthetic.
- Use only values supported by the source unless illustrative values are explicitly identified.
- Prefer a small plot that teaches one concept over a decorative or overloaded figure.

## Python code in notebooks

All function and method signatures must include type annotations.

```python
# Yes
def derivative_of_square(x: float) -> float:
    return 2.0 * x

# No
def derivative_of_square(x):
    return 2.0 * x
```

Additional rules:

- Put imports near the beginning of the notebook and use the dependencies declared in `pyproject.toml`.
- Use descriptive mathematical names and annotate important arrays, especially where shape is not obvious.
- Prefer clear NumPy/SymPy code over clever compact code.
- Avoid hidden state: a clean kernel must run cells successfully from top to bottom.
- Use fixed random seeds and bounded workloads.
- Do not depend on local absolute paths, network access, secrets, or undeclared packages.
- Keep reusable computations in small typed functions; add docstrings when the purpose or convention is not immediately clear.
- Use assertions for important invariants such as expected shapes, probabilities summing to one, or finite results.
- Do not suppress warnings globally merely to make a notebook appear clean.

## Notebook metadata and outputs

- Use notebook format 4 and retain stable cell IDs.
- Use the repository Python kernel metadata (`Python 3 (ipykernel)`, `python3`).
- Store useful, compact outputs that help the lesson, including plots and short tables.
- Remove accidental debug output, noisy logs, widget state, and stale tracebacks.
- Do not hand-edit embedded image data. Re-execute the notebook to regenerate outputs.
- Reference external assets with paths relative to the notebook, normally `assets/<name>`.

## Validation

Before considering a notebook complete:

1. Read it top to bottom for narrative and notation consistency.
2. Restart the kernel and run all cells in order.
3. Confirm there are no exceptions, warnings that indicate a bug, or hidden dependencies on prior state.
4. Check equations against the code and inspect plot labels, legends, and units.
5. Confirm the notebook remains valid JSON and that only intended files changed.

From the repository root, execute a notebook with:

```bash
uv run jupyter nbconvert \
  --to notebook \
  --execute \
  --inplace \
  --ExecutePreprocessor.timeout=120 \
  weeks/<course_week>/<notebook>.ipynb
```

Then inspect the diff and repository status:

```bash
git diff --check
git status --short
```

For Python modules or extracted reusable code, also run:

```bash
uv run ruff check .
uv run pytest
```

## Scope discipline

Do not rewrite unrelated notebooks while preparing one lesson. Preserve user changes already present in the working tree, and do not modify environment, lock, IDE, or ignore files unless the task requires it.
