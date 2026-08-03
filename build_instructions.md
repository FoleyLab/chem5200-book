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

## Commit and Push Changes to GitHub

From the top-level project directory, first check what changed:

```bash
cd /Users/jfoley19/Code/chem5200-book
git status
```

Stage the files you want to include in the commit:

```bash
git add myst.yml references.bib lectures notebooks
```

Or, to stage every changed file in the repository:

```bash
git add .
```

Create a commit with a short descriptive message:

```bash
git commit -m "Update course book content"
```

Push the commit to GitHub:

```bash
git push origin main
```

If pushing over the default SSH remote times out on port 22, switch the remote to GitHub's SSH-over-443 endpoint and push again:

```bash
git remote set-url origin ssh://git@ssh.github.com:443/FoleyLab/chem5200-book.git
git push origin main
```

## Notes

- `--site` builds the Jupyter Book site content.
- `--strict` makes build errors visible and causes the command to fail when MyST reports blocking errors.
- For GitHub Pages, the next steps are to initialize a git repository, add a `.gitignore`, commit the source files, push to GitHub, and add a GitHub Actions workflow that builds and publishes the book.
