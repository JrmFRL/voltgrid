# Readme
  
Pour render le book et le publish:

```
cd docs/science-assessment
quarto publish gh-pages
```
  
C'est tout.

## Alternative : CI/CD GitHub Actions

Au lieu de publier à la main, on peut laisser GitHub rendre et publier à chaque push sur `main`.
`.github/workflows/publish.yml` :

```yaml
on: { push: { branches: main } }
permissions: { contents: write }
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - uses: quarto-dev/quarto-actions/publish@v2
        with: { target: gh-pages, path: docs/science-assessment }
        env: { GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}" }
```
