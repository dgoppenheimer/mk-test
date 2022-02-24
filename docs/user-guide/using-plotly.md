---
title: Using Plotly
---
# Using Plotly

Much of the analysis of MD simulations involves creating plots and graphs to summarize the data. The Python environment of Google Colab provides access to many of most popular plotting programs including `R`, `Matplotlib`, `Seaborn`, `Plotly`, and others. After reading about the pros and cons of the various packages I settled on [Plotly](https://plotly.com/). Plotly is powerful, offers 3D graphing and interactive plots, and has flexible styling for making publication-quality figures. And of course, it runs well in Jupyter notebooks.

## Resources

[Plotly Tutorial for Beginners](https://www.kaggle.com/kanncaa1/plotly-tutorial-for-beginners): Nice examples for most of the types of plots one would use.  
[Plotly Basics](https://learn.co/lessons/plotly-basics): This tutorial explains the code very well.  
[Getting Started with Plotly in Python](https://plotly.com/python/getting-started/): Go to the source for getting Plotly up and running.  
[Data Visualization with Plotly Express](https://www.coursera.org/projects/data-visualization-plotly-express)  
[Getting Plotly working in Jupyter Lab and fastpages](https://colab.research.google.com/github/binnisb/blog/blob/master/_notebooks/2020-04-02-Plotly-in-lab.ipynb)  
[Plotly Express in Python](https://plotly.com/python/plotly-express/)

## Getting Started

- Switch to appropriate Google Account.
- Start a new notebook.
- Make sure you are still in the appropriate account.
- Mount Google Drive.

First, see if Plotly is installed:

```py
import plotly
plotly.__version__
5.5.0 # Plotly 5.5 is already installed in Colab
```

### Saving Images of Plots

I want to include a few images of the plots produced by Plotly. See [Static Image Export in Python](https://plotly.com/python/static-image-export/) for instructions.

```py
pip install -U kaleido
```

!!! warning

    The `pip` installation did not work. I kept getting an error message that `kaleido` was not installed even though it installed successfully. This was solved by installing `kaleido` using `conda`.

```py
!pip install -q condacolab
import condacolab
condacolab.install()
```

Once the kernel reboots, you are good to go.

Okay. Now we can export a plot as an image by including `fig.write_image("fig1.png")` in our code.

### Using Plotly in Colab

Let's plot something. See [IV_Plotly](https://colab.research.google.com/github/pytrain/iViz/blob/master/IV_Plotly.ipynb#scrollTo=2ljXzS-h9Gym) for most of the code, below.

```py
import plotly.graph_objects as go
import numpy as np

fig = go.Figure()

config = dict({'scrollZoom': True})

fig.add_trace(
    go.Scatter(
        x=[1, 2, 3],
        y=[1, 3, 1]))

fig.show(config=config)
fig.write_image("fig1.png")
```

<figure markdown>
  ![test plot using plotly](../assets/images/using-plotly/fig1.png){ width="400" }
  <figcaption>Here is a Plotly plot</figcaption>
</figure>

Let's try another plot.

```py
import plotly.express as px
iris = px.data.iris()
fig = px.scatter(iris, x="sepal_width", y="sepal_length", color="species", marginal_y="violin",
           marginal_x="box", trendline="ols")
fig.show()
fig.write_image("fig2.png")
```

![test plot using plotly](../assets/images/using-plotly/fig2.png){ width="600" }

!!! success

And my favorite--a box plot!

![test plot using plotly](../assets/images/using-plotly/fig3.png){ width="600" }

Let's look at the underlying data as a table.

```py
import plotly.graph_objects as go
import pandas as pd

import plotly.express as px

df = px.data.tips()

fig = go.Figure(data=[go.Table(
    header=dict(values=list(df.columns),
                fill_color='paleturquoise',
                align='left'),
    cells=dict(values=df.values.T,
               fill_color='lavender',
               align='left'))
])

fig.show()
fig.write_image("fig3.png") # make a figure
```

![test plot using plotly](../assets/images/using-plotly/fig4.png){ width="600" }

!!! note

    The table is scrollable in Colab

I uploaded some `.dat` files from RMSD measurements from analyzing an MD trajectory in VMD.

Here is some useful Plotly information:

- `df.index` returns the list of the index, in our case, it’s just integers 0, 1, 2, …, 97.
- `df.columns` gives the list of the column (header) names.

This code:

```py
import plotly.graph_objects as go
import pandas as pd

import plotly.express as px

df = pd.read_csv('/content/rmsd-core.dat',
           sep='\s\s+', engine='python')
           
df.columns
```

Returns: `Index(['frame', 'mol0'], dtype='object')`

```py
df.mol0 # gets the data in the specified column
# this wont work if the column has a space in it
```

```bash
0       NaN
1     0.405
2     0.507
3     0.606
4     0.657
      ...  
93    1.914
94    1.898
95    1.951
96    1.953
97    1.932
Name: mol0, Length: 98, dtype: float64
```

See [Get values in rows and columns in Pandas](https://pythoninoffice.com/get-values-rows-and-columns-in-pandas-dataframe/)

```
dataframe['column name']
```
dataframe = df
use double square brackets for multiple columns

```
dataframe[ ['column name 1', 'column name 2', 'column name 3', ... ] ]
```

`df.loc[row, column]`. column is optional, and if left blank, we can get the entire row.

Let's look at one of the files I uploaded to Colab, `msd-core.dat`.

```py
import plotly.graph_objects as go
import pandas as pd
import plotly.express as px

df = pd.read_csv('/content/rmsd-core.dat',
           sep='\s\s+', engine='python')

# The above code creates a dataframe (df) from reading a csv file.
# our file was not really a csv file, so we need to specify
# the delimiter (spaces, using Regex), and the engine 
# that does the reading

fig = go.Figure(data=[go.Table(
    header=dict(values=list(df.columns),
                fill_color='paleturquoise',
                align='center'),
    cells=dict(values=[df.frame, df.mol0],
                fill_color='lavender',
                align='left'))
])

# The above code creates a figure from the dataframe,
# and styles the header and the cells of the table.

fig.update_layout(width=500) # limits the table to a width of 500px
fig.show() # shows the figure
fig.write_image("rmsd-core.dat.png") # make a png of the figure
```

![a data table](../assets/images/using-plotly/rmsd-core.dat.png){ width="400"}

#### Styling Plots

To make it easier to assign colors to plots, I included a cell that contains code to produce swatches of named colors that will work in Colab. This code comes from the [List of named colors](https://matplotlib.org/stable/gallery/color/named_colors.html) page from the [Matplotlib documentation website](https://matplotlib.org/stable/index.html). I put this code into a form so I can keep it out of the way.

=== "Color Figure"

    ![a data table](../assets/images/using-plotly/named-colors.png)

=== "Code"

    ```py
    #@title Named Colors Code

    """
    ====================
    List of named colors
    ====================

    This plots a list of the named colors supported in matplotlib. Note that
    :ref:`xkcd colors <xkcd-colors>` are supported as well, but are not listed here
    for brevity.

    For more information on colors in matplotlib see

    * the :doc:`/tutorials/colors/colors` tutorial;
    * the `matplotlib.colors` API;
    * the :doc:`/gallery/color/color_demo`.
    """

    from matplotlib.patches import Rectangle
    import matplotlib.pyplot as plt
    import matplotlib.colors as mcolors


    def plot_colortable(colors, title, sort_colors=True, emptycols=0):

        cell_width = 212
        cell_height = 22
        swatch_width = 48
        margin = 12
        topmargin = 40

        # Sort colors by hue, saturation, value and name.
        if sort_colors is True:
            by_hsv = sorted((tuple(mcolors.rgb_to_hsv(mcolors.to_rgb(color))),
                            name)
                            for name, color in colors.items())
            names = [name for hsv, name in by_hsv]
        else:
            names = list(colors)

        n = len(names)
        ncols = 4 - emptycols
        nrows = n // ncols + int(n % ncols > 0)

        width = cell_width * 4 + 2 * margin
        height = cell_height * nrows + margin + topmargin
        dpi = 72

        fig, ax = plt.subplots(figsize=(width / dpi, height / dpi), dpi=dpi)
        fig.subplots_adjust(margin/width, margin/height,
                            (width-margin)/width, (height-topmargin)/height)
        ax.set_xlim(0, cell_width * 4)
        ax.set_ylim(cell_height * (nrows-0.5), -cell_height/2.)
        ax.yaxis.set_visible(False)
        ax.xaxis.set_visible(False)
        ax.set_axis_off()
        ax.set_title(title, fontsize=24, loc="left", pad=10)

        for i, name in enumerate(names):
            row = i % nrows
            col = i // nrows
            y = row * cell_height

            swatch_start_x = cell_width * col
            text_pos_x = cell_width * col + swatch_width + 7

            ax.text(text_pos_x, y, name, fontsize=14,
                    horizontalalignment='left',
                    verticalalignment='center')

            ax.add_patch(
                Rectangle(xy=(swatch_start_x, y-9), width=swatch_width,
                        height=18, facecolor=colors[name], edgecolor='0.7')
            )

        return fig

    plot_colortable(mcolors.BASE_COLORS, "Base Colors",
                    sort_colors=False, emptycols=1)
    plot_colortable(mcolors.TABLEAU_COLORS, "Tableau Palette",
                    sort_colors=False, emptycols=2)

    # sphinx_gallery_thumbnail_number = 3
    plot_colortable(mcolors.CSS4_COLORS, "CSS Colors")

    # Optionally plot the XKCD colors (Caution: will produce large figure)
    # xkcd_fig = plot_colortable(mcolors.XKCD_COLORS, "XKCD Colors")
    # xkcd_fig.savefig("XKCD_Colors.png")

    # to save a copy of this figure
    # plt.savefig('named-colors.png')
    plt.show()


    #############################################################################
    #
    # .. admonition:: References
    #
    #    The use of the following functions, methods, classes and modules is shown
    #    in this example:
    #
    #    - `matplotlib.colors`
    #    - `matplotlib.colors.rgb_to_hsv`
    #    - `matplotlib.colors.to_rgba`
    #    - `matplotlib.figure.Figure.get_size_inches`
    #    - `matplotlib.figure.Figure.subplots_adjust`
    #    - `matplotlib.axes.Axes.text`
    #    - `matplotlib.patches.Rectangle`
    ```




Okay, let's plot some data. I uploaded `.dat` files for three different domains of the Adk protein. We can look at the RMSD of each domain separately.


