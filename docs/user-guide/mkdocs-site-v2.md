

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

```bash
touch .gitignore
echo ".DS_Store" >> .gitignore
echo ".gitignore" >> .gitignore
```

Change site name in `mkdocs.yml`

## Customizing the Site

### Add an `extra.css` file

See [How do I specify custom primary color for mkdocs-material?](https://stackoverflow.com/questions/63017898/how-do-i-specify-custom-primary-color-for-mkdocs-material)  
And [Changing the colors](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/)  
And [Customization](https://squidfunk.github.io/mkdocs-material/customization/)



## Create a Landing Page

[How to add a landing page to a mkdocs doc site using mkdocs-material?](https://stackoverflow.com/questions/63438788/how-to-add-a-landing-page-to-a-mkdocs-doc-site-using-mkdocs-material)

Create an `overrides` directory

Reference this in `mkdocs.yml`

```yaml
 theme:
   custom_dir: overrides
```

Since the custom directory is declared, you need to change 

```py
{% extends "overrides/main.html" %}
```

to

```py
{% extends "main.html" %}
```

in `main-styles.html` and `main.html`

okay, I got most of the home page stuff shown on [Binbash Leverage™ Documentation](https://leverage.binbash.com.ar/)

Now I need to customize it.

Start with the footer.

Compare it to the Material footer.

Try and replace the bin bash items with the material items.

need `overrides/assets/stylesheets` directory
 add the css files

The image is a bit too far to the right
search the css file in the overrides directory 
 change .mdx-hero__image{order:1;transform:translateX(1rem);

 from 4rem to 1rem to move the image to the left a bit

In the `home.html` file there is reference to `config.site_description` that has some text in it. The precedes the text: `Set up in 5 minutes`. It is not clear why the `Set up in 5 minutes` text was not added to `config.site_description`, or why the text in `config.site_description` was not added to `home.html`. Now there are two files to change for the same block of text. 

The `config.site_description` refers to the `mkdocs.yml` file:

```yaml
site_description: >-
  Create a branded static site from a set of Markdown files to host the
  documentation of your Open Source or commercial project
```

Add some more stuff to the `mkdocs.yml` file:

```yaml
site_author: David G Oppenheimer
site_description: >-
  Notes on carrying out and analyzing the results from molecular dynamics simulations

# Copyright
copyright: Copyright &copy; 2022 David G Oppenheimer
```

### Remove the `Get Insiders` Button

Delete the following from `home.html`:

```html
    <a href="{{ 'insiders/' | url }}" title="Material for MkDocs Insiders" class="md-button">
      Get Insiders
    </a>
```

### Change Text on the Landing Page

In `home.html`, make the following changes:

Remove the `Set up in 5 minutes.` text.  
Change `Technical documentation that just works` to `Molecular dynamics simulations for fun and profit`  
Change `Quick Start` to `Get Started`.

Test the site on GitHub.



