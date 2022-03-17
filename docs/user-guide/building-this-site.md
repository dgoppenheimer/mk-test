---
title: Building This Site
---

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

!!! failure

    The deployment of the site to the `gh-pages` branch using gh-actions stopped working after a while. I had never pulled that branch to my local repository, and the build on GitHub pages completed, but showed the following warning. 
    ```bash
    WARNING  -  Version check skipped: No version specified in previous deployment.
    ```
    After trying to get it working (and failing) I decided to switch to manual deployment using `mkdocs gh-deploy --force`.

### Manual Deployment of Site

- Remove the `ci.yml` file from `.github/workflows/` directory.
- Delete the `gh-pages` branch on GitHub.

```bash
git push origin --delete gh-pages
```

- Create a new `gh-pages` branch.

```bash
git checkout gh-pages
git push -u origin gh-pages
git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

- Deploy the site.

```bash
mkdocs gh-deploy --force
```

- Add the `site/` directory to `.gitignore`.
- Check the site at [https://dgoppenheimer.github.io/mk-test/](https://dgoppenheimer.github.io/mk-test/).

!!! success

#### Update

I thought I would try the automatic deployment one more time.

- Move the `ci.yml` file back to `.github/workflows/` directory.

!!! failure

    Still no joy.

- Create a `requirements.txt` file with the following contents (see below).
- Add the `requirements.txt` file to the root of your project directory and add it to version control.

!!! note

    I got the file contents below from the[ Mkdocs developer GitHub repository](https://github.com/squidfunk/mkdocs-material/blob/master/requirements.txt) and modified it for my needs.

!!! example "requirements.txt"

    ```txt
    # Copyright (c) 2016-2022 Martin Donath <martin.donath@squidfunk.com>

    # Permission is hereby granted, free of charge, to any person obtaining a copy
    # of this software and associated documentation files (the "Software"), to
    # deal in the Software without restriction, including without limitation the
    # rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
    # sell copies of the Software, and to permit persons to whom the Software is
    # furnished to do so, subject to the following conditions:

    # The above copyright notice and this permission notice shall be included in
    # all copies or substantial portions of the Software.

    # THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    # IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    # FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
    # AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    # LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
    # FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
    # IN THE SOFTWARE.

    # Direct dependencies
    jinja2>=2.11.1
    markdown>=3.2
    mkdocs>=1.2.3
    mkdocs-video>=1.1.0
    mkdocs-material>=8.0
    mkdocs-material-extensions>=1.0
    pygments>=2.10
    pymdown-extensions>=9.0

    ```

Create a `gh-pages.yml` file with the contents listed below and put it into the `.github/workflows/` directory.

I got this `gh-pages.yml` file from [peaceiris' action-gh-pages GitHub repository](https://github.com/peaceiris/actions-gh-pages#%EF%B8%8F-static-site-generators-with-python)

Contents of the `gh-pages.yml` file:

```yaml
name: GitHub Pages

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v2

      - name: Setup Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.8'

      - name: Upgrade pip
        run: |
          # install pip=>20.1 to use "pip cache dir"
          python3 -m pip install --upgrade pip

      - name: Get pip cache dir
        id: pip-cache
        run: echo "::set-output name=dir::$(pip cache dir)"

      - name: Cache dependencies
        uses: actions/cache@v2
        with:
          path: ${{ steps.pip-cache.outputs.dir }}
          key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
          restore-keys: |
            ${{ runner.os }}-pip-

      - name: Install dependencies
        run: python3 -m pip install -r ./requirements.txt

      - run: mkdocs build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.ref == 'refs/heads/main' }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site
```



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

No joy.

Add `site_url: https://dgoppenheimer.github.io/mk-test/` to `mkdocs.yml`.

!!! success

### Change Colors on the Landing Page

The lower purple is okay, but I want to see how it looks with a lighter blue on top.

Add this to `mkdocs.yml`:

```yaml
  palette:
    primary: blue
```

!!! info
    So far, so good.

### Adjust Header

I want to remove the `For updates follow @squidfunk on Twitter` banner from the top of the Landing Page. This is declared in the `docs/overrides/main.html` file. Delete the following:

```html
{% block announce %}
  <a href="https://twitter.com/squidfunk">
    For updates follow <strong>@squidfunk</strong> on
    <span class="twemoji twitter">
      {% include ".icons/fontawesome/brands/twitter.svg" %}
    </span>
    <strong>Twitter</strong>
  </a>
{% endblock %}
```

The footer is missing from the front page, but that's okay--it's not really needed.

### Change the favicon and logo

See [Changing the logo and icons](https://squidfunk.github.io/mkdocs-material/setup/changing-the-logo-and-icons/) for instructions.

Add files to the appropriate directories and add this to `mkdocs.yml`:

```yaml
theme:
  logo: assets/logo.svg
  favicon: assets/images/favicon.png
```

!!! success

    Worked like a charm.

## Changing Page Title

The `nav` part of `mkdocs.yml` takes precedence when setting the page title. But I want a longer title on the page and a shorter one for the navigation links. I found this solution in the [mkdocs issues](https://github.com/mkdocs/mkdocs/issues/1795). Put this code in your `/overrides/main.html` file.

```jinja
{% extends "base.html" %}
{% if page.toc|first is defined %}
{% set _title = page.toc.items[0].title %}
{% else %}
{% set _title = page.title|striptags %}
{% endif %}

{% block htmltitle %}
<title>{{ _title }}</title>
{% endblock %}
```

## Navigation

See [Setting up navigation](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/) in the Material theme documentation for excellent instructions.

### Anchor Tracking

Add the following to the `mkdocs.yml`:

```yaml
theme:
  features:
    - navigation.tracking
```

### Navigation Tabs

Add the following to the `mkdocs.yml`:

```yaml
theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky
```

### Back to Top Button

Add the following to the `mkdocs.yml`:

```yaml
theme:
  features:
    - navigation.top
```

Okay, all these features so far are working perfectly. The rest is pretty straightforward--just add and organize content.

### Tags

I'm not sure that the tags feature will be useful on this site. I say this because the search feature provided by MkDocs and the Material theme appears to be excellent.

Add the following to the `mkdocs.yml`:

```yaml
markdown_extensions:
  - meta
plugins:
  - tags
```

### Footnotes

```yaml
markdown_extensions:
  - footnotes
```


### MathJax

```js
$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$
```


$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$

## Plugin for Video

[mkdocs-video plugin](https://github.com/soulless-viewer/mkdocs-video)

Images used for Jupyter need an odd syntax, but local images can be standard Markdown. Also can use html in markdown.

### Usage

```markdown
![type:video](https://www.youtube.com/embed/LXb3EKWsInQ)
```

## Image Captions

[markdown_captions](https://github.com/Evidlo/markdown_captions)

Install using `pip`.

```bash
pip install markdown-captions
```

Use the extension as follows.

Also using the Markdown extension, `attr_list`.

```markdown
![image caption](https://github.com/dgoppenheimer/notebook-images/blob/main/g-create.png?raw=true){: style="height:150px;width:150px""}
```

Add the following to `mkdocs.yml`:

```yaml
markdown_extensions:
  - markdown_captions
```

![image caption](https://github.com/dgoppenheimer/notebook-images/blob/main/g-create.png?raw=true){: style="height:150px;width:150px"}

Herp derpsum merpus ler derperker herpderpsmer. Pee sherper dee serp. Merpus re se ter derpsum me sherper herpler. Cerp herp derpy herpderpsmer tee. Herpem de mer, zerpus derpler sherpus der herpderpsmer ner. Merpus nerpy sherlamer derp! Me der berps, derp sherlamer. Ner derpsum se derpler nerpy. Derperker se derpus perper sherper. Re nerpy de derps ter. Herpderpsmer ler derpy ner pee derpsum herpem, cerp berp? Serp er zerpus merp berps terpus derperker cerp ler derp? Sherlamer derpler re, sherp derpus. Mer ner serp derpus cerp derpler ler perper. Herderder derp derpsum mer!

You can see that `markdown_captions` cannot use the `attr_list` without making a mess of the resulting figure and caption.

From the [Images section](https://squidfunk.github.io/mkdocs-material/reference/images/#image-alignment) of the Material documentation:

```html
<figure markdown>
  ![Image title](https://dummyimage.com/600x400/){ width="300" align="right"}
  <figcaption>Image caption</figcaption>
</figure>
```

<figure markdown>
  ![Image caption](https://dummyimage.com/600x400/){ width="300", align="right"}
  <figcaption>Image caption</figcaption>
</figure>

With no width attribute:

<figure markdown>
  ![Image caption](https://dummyimage.com/600x400/)
  <figcaption>Image caption</figcaption>
</figure>

Below, image caption and left alignment was specified.

```html
<figure markdown>
  ![alt](https://dummyimage.com/250x250/){ align="left" }
  <figcaption>Image caption</figcaption>
</figure>
```

<figure markdown>
  ![alt](https://dummyimage.com/250x250/){ align="left" }
  <figcaption>Image caption</figcaption>
</figure>

Herp derpsum merpus ler derperker herpderpsmer. Pee sherper dee serp. Merpus re se ter derpsum me sherper herpler. Cerp herp derpy herpderpsmer tee. Herpem de mer, zerpus derpler sherpus der herpderpsmer ner. Merpus nerpy sherlamer derp! Me der berps, derp sherlamer. Ner derpsum se derpler nerpy. Derperker se derpus perper sherper. Re nerpy de derps ter. Herpderpsmer ler derpy ner pee derpsum herpem, cerp berp?

But the alignment does not work.

It looks like the alignment will work only within `markdown`, but not within `html`.

```markdown
![Image title](https://dummyimage.com/200x200/eee/aaa){ align="left" }
```

Renders to:

![Image title](https://dummyimage.com/200x200/eee/aaa){ align="left" }

Herp derpsum merpus ler derperker herpderpsmer. Pee sherper dee serp. Merpus re se ter derpsum me sherper herpler. Cerp herp derpy herpderpsmer tee. Herpem de mer, zerpus derpler sherpus der herpderpsmer ner. Merpus nerpy sherlamer derp! Me der berps, derp sherlamer. Ner derpsum se derpler nerpy. Derperker se derpus perper sherper. Re nerpy de derps ter. Herpderpsmer ler derpy ner pee derpsum herpem, cerp berp?

But you don't get a caption.

<br/>
<br/>
<br/>
<br/>


![Image title](https://dummyimage.com/400x400/eee/aaa){ align="left" }

Herp derpsum merpus ler derperker herpderpsmer. Pee sherper dee serp. Merpus re se ter derpsum me sherper herpler. Cerp herp derpy herpderpsmer tee. Herpem de mer, zerpus derpler sherpus der herpderpsmer ner. Merpus nerpy sherlamer derp! Me der berps, derp sherlamer. Ner derpsum se derpler nerpy. Derperker se derpus perper sherper. Re nerpy de derps ter. Herpderpsmer ler derpy ner pee derpsum herpem, cerp berp?

<br/>
<br/>
<br/>
<br/>

For Google Colab images, using `markdown` in `html` allows both resizing the image and specifying its alignment. But you still don't get a caption.

```html
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true" alt="connect to a runtime" width="250" align="right"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true)
```

[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true" alt="connect to a runtime" width="250" align="right"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true)

One last attempt.

```html
<figure markdown>
  ![<img src="https://dummyimage.com/600x400/" alt="dummy image" width="250" align="right"/>](https://dummyimage.com/600x400/)
  <figcaption>Caption: this image should be small and on the right</figcaption>
</figure>
```

<figure markdown>
  [<img src="https://dummyimage.com/600x400/" alt="dummy image" width="250" align="right"/>](https://dummyimage.com/600x400/)
  <figcaption>Caption: this image should be small and on the right</figcaption>
</figure>

<figure markdown>
  [<img src="https://dummyimage.com/600x400/" alt="dummy image" width="250"/>](https://dummyimage.com/600x400/)
  <figcaption>Caption: this image should be small in the center</figcaption>
</figure>

#### a locally served image

```mk
![an image](../assets/images/using-plotly/fig1.png){ width="300" }
```

Renders to 

![an image](../assets/images/using-plotly/fig1.png){ width="300" }

```html
<figure markdown>
  ![alt](../assets/images/using-plotly/fig1.png){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>
```

Renders to 

<figure markdown>
  ![alt](../assets/images/using-plotly/fig1.png){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>

!!! note

    Okay, this is not perfect, but works well enough. I can get images and resize them for the Jupyter notebooks, and I can serve local images for testing purposes. I can get captions and alignment some of the time.





