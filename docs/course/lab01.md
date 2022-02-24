---
date: 2022-01-28
---

# Lab 01: Introduction to Jupyter notebooks and Colab

[<img  width="50" src="https://drive.google.com/uc?export=view&id=1-JE5lbCK4Amelom8clmAyXUOAoyHhfiq" alt="Colaboratory logo" align="left" hspace="10" vspace="30" /> ](https://drive.google.com/uc?export=view&id=1-JE5lbCK4Amelom8clmAyXUOAoyHhfig)

## Welcome to Google Colaboratory!

*In this exercise you will learn about Jupyter notebooks and Google Colaboratory (Colab).*

What is Google Colaboratory?

[Google Colaboratory](https://colab.research.google.com/) (or “Colab” for short) is a cloud-based platform that allows users to run software on high-performance computer clusters for free. Colab uses the [Jupyter notebook](https://jupyter.org/) format, which allows users to create and store code, computing output, visualizations, and text within a web browser.

Watch the video, below, to get a brief introduction to what Colab offers.

![type:video](https://www.youtube.com/embed/inN8seMm7UI)

## Jupyter Notebooks

[Jupyter](https://jupyter.org/) notebooks are documents that allow you to create, view, and run code. These notebooks are typically web-based and can contain code, text, equations, images, videos, and more. The document you are reading now is a Jupyter notebook. Importantly, these notebooks are interactive--you can change the code, run it and view the new output. Also, you can store the output of the code in the notebook and share it with others. This abilitly to document what code you executed, and the resulting output is important for recproducibility. 

Jupyter notebooks can be run locally on your own computer, and can use many different programming languages. However, we will be used a web-based notebook that uses the [python](https://www.python.org/) language.

### Cells

Jupyter notebooks are made up of two kinds of cells: **code cells** and **text cells**. 

#### Adding and moving cells

New code or text cells can be added by using the `+ CODE` and `+ TEXT` buttons that show up when you hover at the bottom of a cell. You can also find these buttons in the toolbar above the notebook.

[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/add-cells.png?raw=true" alt="add cells" width="560"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/add-cells.png?raw=true)

You can move a cell by selecting it and clicking the up arrow button(which moves selected cell up) or the down arrow button (which moves the selected cell down) in the toolbar in the upper right of a selected cell.

[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/move-cells.png?raw=true" alt="move cells" width="560"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/move-cells.png?raw=true)

#### Text Cells

Text cells are used to annotate your code, describe your workflow, provide instructions, or add additional information to your notebook. Text cells are formatted using [Markdown](https://daringfireball.net/projects/markdown/), a text to `html` conversion tool widely used to format text on the web. With Markdown, you can add text formatting such as **bold** and *italics*, add images, links, and more!

For more information, please visit the [Markdown Guide](https://www.markdownguide.org/), especially the [Getting Started](https://www.markdownguide.org/getting-started/) section. We will be using Markdown throughout this course to format our text cells.

#### Code Cells

Below is a code cell. Once the toolbar button indicates `CONNECTED`, click in the cell to select it and execute the contents in the following ways:

- Click the `Play` icon in the upper left corner of the code cell; it will appear when you hover over the `[ ]`.
- Type `Cmd/Ctrl+Enter` to run the cell in place
- Type `Shift+Enter` to run the cell and move to the next cell. A new cell will be added if there are no remaining cells.
- Type `Alt+Enter` to run the cell and insert a new code cell immediately below it.

Additional options for running some or all cells in your notebook can be found in the `Runtime` menu.

```py
# This is a comment in a code cell
# It is preceded by a hash symbol (#)
# Comments are useful for annotating parts of your code
# Comments are ignored when the code cell is run
codons = 154
protein_MW = codons * 110
print(protein_MW)
```



Click the button, Open in Colab
Run the cell, Mount Google Drive
Wait until the notebook connects with Google's computers

g-create
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/g-create.png?raw=true" alt="create account" width="560"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/g-create.png?raw=true)

#### g-create using extension to control size

![test](https://github.com/dgoppenheimer/notebook-images/blob/main/g-create.png?raw=true){: style="height:150px;width:150px""}

mount-drive
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/mount-drive.png?raw=true" alt="mount Google Drive" width="560"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/mount-drive.png?raw=true)

run-anyway
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/run-anyway.png?raw=true" alt="add cells" width="560"/>](https://github.com/dgoppenheimer/notebook-images/blob/main/run-anywa.png?raw=true)

#### run-anyway Left

![Image title](https://dummyimage.com/200x200/eee/aaa){ align=left }

Herp derpsum merpus ler derperker herpderpsmer. Pee sherper dee serp. Merpus re se ter derpsum me sherper herpler. Cerp herp derpy herpderpsmer tee. Herpem de mer, zerpus derpler sherpus der herpderpsmer ner. Merpus nerpy sherlamer derp! Me der berps, derp sherlamer. Ner derpsum se derpler nerpy. Derperker se derpus perper sherper. Re nerpy de derps ter. Herpderpsmer ler derpy ner pee derpsum herpem, cerp berp? Serp er zerpus merp berps terpus derperker cerp ler derp? Sherlamer derpler re, sherp derpus. Mer ner serp derpus cerp derpler ler perper. Herderder derp derpsum mer!


![run anyway](https://github.com/dgoppenheimer/notebook-images/blob/main/run-anyway.png?raw=true){ align=left }

<figure markdown>
  ![Run anyway](https://github.com/dgoppenheimer/notebook-images/blob/main/run-anyway.png?raw=true){ width="560" }
</figure>

(You may need to mount your drive, again)

