

```bash
pip install mkdocs-material

cd ~/Sites
mkdir mk-test
cd mk-test
mkdocs new .

```

Add to `config.yml`:

```yaml
theme:
  name: material
```

## Publishing the Site

From [Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)

Create `.github/workflows/ci.yml`

```yaml
name: ci 
on:
  push:
    branches:
      - master 
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs-material 
      - run: mkdocs gh-deploy --force
```

```bash
git init
git status
git add .
git commit -m "initial commit"
```

Create a new repository on GitHub.

```bash
git remote add origin https://github.com/dgoppenheimer/mk-test.git
git branch -M main
git push -u origin main
```

Go to `https://github.com/dgoppenheimer/mk-test/settings/pages`

Choose `gh-pages` branch and click `Save`.

Add some text to `index.md`

Save, commit and `git push`

go to `https://github.com/dgoppenheimer/mk-test/actions` and watch the site being built.

Check the site at `https://dgoppenheimer.github.io/mk-test/`

Add to mkdocs.yml

```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```

!!! success


Create a directory and a file

```
cd docs
mkdir user-guide
```

!!! success

