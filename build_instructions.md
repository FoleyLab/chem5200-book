# Build Instructions

This project is a Jupyter Book 2 / MyST book. The working conda environment is:

```bash
/Users/jfoley19/miniforge3/envs/chem5200
```

## Build the Site Locally

From the top-level project directory:

```bash
cd /Users/jfoley19/Code/chem5200-book
conda activate /Users/jfoley19/miniforge3/envs/chem5200
jupyter-book build --site --strict
```

If running without activating the environment, put the environment's `bin` directory first on `PATH`:

```bash
cd /Users/jfoley19/Code/chem5200-book
PATH=/Users/jfoley19/miniforge3/envs/chem5200/bin:$PATH jupyter-book build --site --strict
```

## Preview Locally

```bash
cd /Users/jfoley19/Code/chem5200-book
conda activate /Users/jfoley19/miniforge3/envs/chem5200
jupyter-book start
```

## Notes

- `--site` builds the Jupyter Book site content.
- `--strict` makes build errors visible and causes the command to fail when MyST reports blocking errors.
- For GitHub Pages, the next steps are to initialize a git repository, add a `.gitignore`, commit the source files, push to GitHub, and add a GitHub Actions workflow that builds and publishes the book.
