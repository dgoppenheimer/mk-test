---
title: Conda on Colab
date: 2022-02-05
description: A quick guide to installing Conda on Google Colab
---

Some packages recommend using `conda` for installation on Google Colab. Here is a quick guide to doing so.

See [How to install / use Conda on Google Colab](https://inside-machinelearning.com/en/how-to-install-use-conda-on-google-colab/), a guide to installing Conda when using Google Colab.

Check to see if conda is already installed:

```py
!conda --version
```

You may get the error:

!!! failure "Error"

    ```bash
    /bin/bash: conda: command not found
    ```

To fix, install conda:

```py
!pip install -q condacolab
import condacolab
condacolab.install()
```

Note that the kernel will reboot and you will see this error message:

!!! warning 

    Your session crashed for an unknown reason.
    
It is okay to dismiss this notice.

Confirm that installation was successful:

```py
!conda --version
```

You should get `conda 4.9.2`, or whatever the current version is.

!!! success

Now you can use conda for installation of other packages that are not available by `pip` or that run better after installation with `conda`.
