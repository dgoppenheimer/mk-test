---
date: 2022-02-19
---

# Lab 00: Preparation for Molecular Dynamics

*This article outlines the requirements you will need to begin using Jupyter notebooks and Google Colaboratory (Colab).*

## Learning Objectives

By the end of this exercise, you will be able to do the following:

- Sign up for an additional personal Google account that will be used for this course.
- Download and install the Google Chrome web browser.
- Use the provided workflow for accessing and saving course notebooks.

## Requirements

To complete the assignments for this course, you will need the following:

### Requirement 1: A Molecular Dynamics Google account

This will allow you to save your notebooks to a dedicated Google Drive that does not have any personal or UF files on it. Below are the instructions for getting your personal Molecular Dynamics Google account.

1. Go to [Google.com](https://www.google.com/) and click `Sign in`, then `Create account`.

- If you already have a Google account, Click on your profile picture, then click on `Add another account`.

{{< imgproc g-account-profile.png Resize "550x" >}}
Click profile
{{< /imgproc >}}

{{< imgproc add-account.png Resize "350x" >}}
Add another account
{{< /imgproc >}}

- Then click `Create account` and `For myself`

2. Fill in the appropriate information for your `First name`, `Last name`, and `Password`. For the `Username`, use the following format: `<last name><first initial>.mdynamics`, but do not use spaces or the `< >` characters, and notice the `dot` before `mdynamics`. For example, my `Username` is:

```bash
oppenheimerd.mdynamics@gmail.com
```

3. Follow the remaining instructions and you should be ready to go.

### Requirement 2: A Chrome web browser

Working with colab and Google drive (G-drive) works best in the [Chrome](https://www.google.com/chrome/) web browser. If you don't already have it installed, go to the [Chrome download page](https://www.google.com/chrome/) to download and install it on your computer.

{{% alert title="Note" color="primary" %}}
You can also use the Firefox browser, but you must sign in to the correct Google account once you launch the notebook.
{{% /alert %}}

<mark>**Always use your mdynamics Google account to complete these assignments**.</mark>

## Workflow Summary

Here is a quick summary of how you will access course materials. Additional detailed instructions can be found below the summary.

1. Go to the [Molecular Dynamics GitHub repository](https://github.com/dgoppenheimer/Molecular-Dynamics) to access the Jupyter notebooks that contain the tutorials and assignments.
2. Choose the assignment you want to work on and click the ![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg) button. The notebook will open in your (Chrome) web browser.
3. Change accounts to your `<last name><first initial>.mdynamics@gmail.com` account.
4. Connect to a runtime and mount your G-drive.
5. Save a copy of the notebook to your G-drive.
6. Rename the notebook by prepending `<last name><first initial>-` (without the spaces or `<` `>` characters) to the notebook name. For example: `oppenheimerd-Lab01-intro-jupyter.ipynb`.

### Slightly More Detailed Workflow Instructions

1. Open your web browser and go to the [Molecular Dynamics GitHub repository](https://github.com/dgoppenheimer/Molecular-Dynamics). Scroll down to the *Practical Molecular Dynamics* `README.md` section to see the table listing all the assignments.
2. Click the ![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg) button to open the notebook you want to work on.
3. Sign in (or change accounts) to your `<last name><first initial>.mdynamics@gmail.com` account.
4. Connect to a runtime by clicking the `Connect` button. You should be connected to Google's computers in a few seconds. Then mount your G-drive.

{{< imgproc connect.png Resize "750x" >}}
Connect to a runtime
{{< /imgproc >}}

{{< imgproc connected.png Resize "750x" >}}
Connected!
{{< /imgproc >}}

{{< imgproc mount-g-drive.png Resize "750x" >}}
Mount your G-drive
{{< /imgproc >}}

When asked `Permit this notebook to access your Google Drive files?`, click the `Connect to Google Drive` button. In the next popup window, choose your `last name><first initial>.mdynamics@gmail.com` account.

{{< imgproc choose-account.png Resize "450x" >}}
choose your mdynamics@gmail.com account
{{< /imgproc >}}

Click `Allow` when asked by Google Drive for desktop wants to access your Google Account.

{{< imgproc allow-access.png Resize "350x" >}}
Allow access
{{< /imgproc >}}

When the cell is done running and your G-drive is mounted, you should see `Mounted at /content/drive` in the output area of the cell.

5. Save a copy of the notebook to your G-drive. Click the folder icon on the left of the notebook to see your mounted drive and other files that you can access in this notebook.

{{< imgproc folder-icon.png Resize "550x" >}}
Click the folder icon
{{< /imgproc >}}

{{< imgproc files.png Resize "550x" >}}
See your files!
{{< /imgproc >}}

6. Rename the notebook by prepending `<last name><first initial>-` (without the spaces or `<` `>` characters) to the notebook name. For example: `oppenheimerd-Lab01-intro-jupyter.ipynb`.

{{< imgproc rename-notebook.png Resize "550x" >}}
Rename your notebook
{{< /imgproc >}}

Once your notebook is renamed, save a copy to your G-drive.

---

## Code for Images in Jupyter Notebooks

I use Hugo shortcodes for processing images on this site to keep the markdown clean. The images are stored in `page bundles` for use on this site. I also uploaded all the images to a public GitHub repository, [notebook-images](https://github.com/dgoppenheimer/notebook-images), so I can use them with the Jupyter notebooks. Using a public repository ensures that the images will still be available when the notebook is shared.

Here is the code I used to generate the images in the Jupyter notebooks. This code is a bit different from standard Markdown in that it allows the images to be resized rather than just filling the container.

{{% alert title="Information" color="info" %}}
Code for the Jupyter notebook:  
*Click profile*

```html
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/g-account-profile.png?raw=true" alt="Profile picture" width="350" />](https://github.com/dgoppenheimer/notebook-images/blob/main/g-account-profile.png?raw=true)
```

*Add another account*

```html
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/add-account.png?raw=true" alt="add another account" width="250" />](https://github.com/dgoppenheimer/notebook-images/blob/main/add-account.png?raw=true)
```

*Connect to a runtime*

```html
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true" alt="connect to a runtime" width="750" />](https://github.com/dgoppenheimer/notebook-images/blob/main/connect.png?raw=true)
```

*Connected!*

```html
[<img src="https://github.com/dgoppenheimer/notebook-images/blob/main/connected.png?raw=true" alt="connected" width="750" />](https://github.com/dgoppenheimer/notebook-images/blob/main/connected.png?raw=true)
```

{{% /alert %}}
