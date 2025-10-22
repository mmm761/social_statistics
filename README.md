# Your Sexy R Book (Quarto)

A minimal Quarto book with R chunks, perfect for GitHub Pages.

## Quick start

1. Install Quarto (https://quarto.org). In RStudio, update to a version that supports Quarto.
2. In R, ensure **knitr** is installed: `install.packages("knitr")`.
3. Build locally:

   ```bash
   quarto render
   ```

4. Serve locally (live reload while you edit):

   ```bash
   quarto preview
   ```

5. Publish to GitHub Pages:
   - Commit & push to GitHub.
   - In Settings → Pages, choose `GitHub Actions`.
   - Add the provided Quarto workflow (see below).

## GitHub Actions (optional)

Create `.github/workflows/publish.yml` with:

```yaml
name: Publish Quarto Book
on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - uses: r-lib/actions/setup-r@v2
      - name: Install R deps
        run: |
          R -q -e 'install.packages(c("knitr","rmarkdown","dplyr","ggplot2"))'
      - name: Render
        run: |
          quarto render
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: _book
```

## Bookdown variant (optional)

If you prefer classic **bookdown**, keep `_bookdown.yml` and `_output.yml`, and create `index.Rmd` etc.
But Quarto is the modern path and works great with R.
```

