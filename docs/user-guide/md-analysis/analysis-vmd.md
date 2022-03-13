---
title: Analysis in VMD
---

# Analyzing a Trajectory in VMD

For this exercise, I'll follow the [PHY542: MD analysis with VMD tutorial](https://becksteinlab.physics.asu.edu/pages/courses/2017/PHY542/practicals/md/dynamics/index.html).

I downloaded the needed files from the [Input files for PHY542 MD Practical](https://becksteinlab.physics.asu.edu/pages/courses/2016/PHY542/practicals/md/files/).

## Getting Started

First, run (type into the `tcl` console) `logfile console` so that any GUI commands get logged in the console so I can see the corresponding `cli` command.

- Load the topology file. 
    - Go to the *Molecule File Browser* &#8594; *Browse*.
    - Choose `adk.psf`.
    - Click *Load*.

- Load the trajectory file. 
    - Go to the *Molecule File Browser* &#8594; *Load files for* 
    - Choose `0:adk.psf`. 
    - Go to *Browse* and choose `adk_dims.dcd`.
    - Under *Frames*, click *Load all at once*.
    - Click *Load*.

- Play the trajectory for fun.
- Make some new representations.
    - In the `tcl` console type:

```py  
mol addrep 0 # adds a representation of molecule 0
mol modselect 1 0 protein and resid 30 to 59 # changes this representation to just the NMP domain of AdK
mol modstyle 1 0 newcartoon
mol modcolor 1 0 ColorID 22 # cyan3


mol addrep 0 # adds another representation of molecule 0
mol modselect 2 0 protein and resid 122 to 159 # LID domain of AdK
mol modstyle 2 0 newcartoon
mol modcolor 2 0 ColorID 17 # yellow3

mol addrep 0 # adds another representation of molecule 0
mol modselect 3 0 protein and not (resid 30 to 59 122 to 159) or (protein and resid 1 to 29 60 to 121 160 to 214) # CORE domain of AdK
mol modstyle 3 0 newcartoon
mol modcolor 3 0 ColorID 6

mol showrep 0 0 off # turn off molecule 0 (top)
```

## RMSD fitting and analysis of a trajectory

### Superposition and RMSD

#### CORE Domain

- Superimpose all trajectory frames on the *CORE* domain.
    - In the `tcl` console type: `menu rmsdtt on`.
    - In the *RMSD Trajectory Tool*:
        - add `protein and not (resid 30 to 59 122 to 159)` (the *CORE* domain) to the box in the upper left of the widget.
        - Choose `Backbone` for *Selection Modifiers*.
        - Choose `Top` for *Reference Mol*.
    - Run *RMSD*. Note that the average RMSD is about 2.651&#177;0.996.
    - Click the box for *On/Off Frame ref:* and use frame `0` for the reference.
    - Run *Align*.
    - Run *RMSD* again. Note that teh RMSD is now 1.521&#177;0.399.
    - In the *RMSD Trajectory Tool*, go to *File* &#8594; *Plot data*.

#### LID Domain

- Superimpose all trajectory frames on the *LID* domain.
    - In the `tcl` console type: `menu rmsdtt on`.
    - In the *RMSD Trajectory Tool*:
        - add `protein and resid 122 to 159` (the *LID* domain) to the box in the upper left of the widget.
        - Choose `Backbone` for *Selection Modifiers*.
        - Choose `Top` for *Reference Mol*.
    - Run *RMSD*. Note that the average RMSD is about 9.921&#177;4.436.
    - Click the box for *On/Off Frame ref:* and use frame `0` for the reference.
    - Run *Align*.
    - Run *RMSD* again. Note that teh RMSD is now 1.013&#177;0.202.
    - In the *RMSD Trajectory Tool*, go to *File* &#8594; *Plot data*.

#### NMP Domain

- Superimpose all trajectory frames on the *NMP* domain.
    - In the `tcl` console type: `menu rmsdtt on`.
    - In the *RMSD Trajectory Tool*:
        - add `protein and resid 30 to 59` (the *NMP* domain) to the box in the upper left of the widget.
        - Choose `Backbone` for *Selection Modifiers*.
        - Choose `Top` for *Reference Mol*.
    - Run *RMSD*. Note that the average RMSD is about 13.085&#177;7.081.
    - Click the box for *On/Off Frame ref:* and use frame `0` for the reference.
    - Run *Align*.
    - Run *RMSD* again. Note that teh RMSD is now 1.342&#177;0.321.
    - In the *RMSD Trajectory Tool*, go to *File* &#8594; *Plot data*.


 using Extensions ‣ Analysis ‣ RMSD Trajectory Tool

















1. `trj_nos.dcd`, which is the short form of `covid-spike-6vxx_1_1_1_traj_dcd`. Before loading, set the stride to 10 (every 10th frame will be loaded), otherwise my laptop runs out of memory and VMD crashes. With `stride=2`, the spike protein trajectory loaded with 642 frames.
2. `prot_gly_memb.psf`

!!! note

    Load the `*.dcd` file first. You may be able to load all the frames depending on the size of the trajectory file and your computer's memory. If you load the `*.psf` or a `*.pdb` file first, and then load the trajectory, the viewer will try to display each frame as it is loaded, which will likely lead to memory problems and a crash. However, the [PHY542: MD analysis with VMD tutorial](https://becksteinlab.physics.asu.edu/pages/courses/2017/PHY542/practicals/md/dynamics/visualization.html) states:
    >You always load a topology file first and then you load the trajectory data for the system.

    I need to check the VMD documentation to determine the correct order for loading the files into VMD.




Turn of the axes from the viewer: type `axes location off` into the `tcl` console.

Let's start by making some new representations so that we can turn off the things we don't want to see in our final image.

## Add a Lipid Representation

```py
mol addrep 0 # adds a representation of molecule 0
mol showrep 0 0 off # turn off molecule 0 (top)
mol modselect 1 0 protein # changed selection for rep 1 to just protein

mol modstyle 1 0 NewCartoon
menu rmsdtt on # turn on the RMSD trajectory tool
```

Click `plot` and `noh` in the `RMSD trajectory tool` menu. Use `0` as the reference frame, and click `align`. Next click `RMSD`.




I looked in the topology file `top_all36_lipid.rtf` to find all the lipid names.

```py
resname DLPC or resname LPPC or resname DLPE or resname DLPS or resname DLPA or resname DLPG or resname DMPC or resname DMPE or resname DMPS or resname DMPA or resname DMPG or resname DPPC or resname DPPE or resname DPPS or resname DPPA or resname DPPG or resname DSPC or resname DSPE or resname DSPS or resname DSPA or resname DSPG or resname DOPC or resname DOPE or resname DOPS or resname DOPA or resname DOPG or resname POPC or resname POPE or resname POPS or resname POPA or resname POPG or resname SAPC or resname SDPC or resname SOPC or resname DAPC
```


Using the `atomselect` command.


A quick test:

```py
set sel [atomselect top "resname DLPC"]
atomselect2
```

```py
atomselect macro lipid {
 resname DLPC or resname LPPC or resname DLPE or resname DLPS or resname DLPA or resname DLPG or resname DMPC or resname DMPE or resname DMPS or resname DMPA or resname DMPG or resname DPPC or resname DPPE or resname DPPS or resname DPPA or resname DPPG or resname DSPC or resname DSPE or resname DSPS or resname DSPA or resname DSPG or resname DOPC or resname DOPE or resname DOPS or resname DOPA or resname DOPG or resname POPC or resname POPE or resname POPS or resname POPA or resname POPG or resname SAPC or resname SDPC or resname SOPC or resname DAPC
}

mol showrep 0 0 off # turn off molecule 0 (top)
mol modselect 1 0 {lipid} # changed selection for rep 1 to just lipid
mol modstyle 1 0 Lines # was the default rep_number mol_number
```

```py
mol showrep 0 0 on # turns on molecule 0, rep 0 (everything)
mol showrep 0 1 off # turns off lipid
mol addrep 0
mol modselect 2 0 protein
mol showrep 0 0 off # turns off "all" rep
# just protein is remaining
mol showrep 0 2 off # turns off protein
mol showrep 0 0 on
```



set sel [atomselect top "protein"]



- `mol showrep molecule_number rep_number [on | off]`

---

Here is the topology file: `top_all36_carb.rtf`

Each carbohydrate is preceded by `RESI` followed by an abbreviation of its name.

I want to print out all of the `RESI` lines with the abbreviated names.

we wish to print all the lines whose fourth column says HIS, we just use:

```bash
awk '$4=="HIS"' 6ane.txt
```

### Using `awk`

>By default Awk prints every line of data from the specified file.  

See [AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)

Print the lines that match a pattern:

```bash
awk '/manager/ {print}' employee.txt 
```

I want to match a pattern of `RESI` followed by a space and 4 capital letters.

Regular expressions to the rescue!

| character | function                                          |
| :-------: | ------------------------------------------------- |
| \s        | Selects any whitespace character                  |
| \w        | Selects any word                                  |
| [a-d]     | Selects any character a through d (a, b, c, or d) |
| [:upper:] | Uppercase alphabetic characters                   |

>For each record i.e line, the awk command splits the record delimited by whitespace character by default and stores it in the $n variables. If the line has 4 words, it will be stored in $1, $2, $3 and $4 respectively. Also, $0 represents the whole line.  

This should print the first and second columns of all records (lines) that start with `RESI`.

```bash
awk '/RESI/ {print $1,$2}' top_all36_carb.rtf
# output
RESI AGLC
RESI BGLC
RESI AALT
RESI BALT
RESI AALL
RESI BALL
RESI AGAL
RESI BGAL
RESI AGUL
RESI BGUL
RESI AIDO
RESI BIDO
RESI AMAN
RESI BMAN
RESI ATAL
RESI BTAL
RESI AXYL
RESI BXYL
RESI AFUC
RESI BFUC
RESI ARHM
RESI BRHM
RESI AGLCA
RESI BGLCA
RESI BGLCA0
RESI AIDOA
RESI BIDOA
RESI AGLCNA
RESI BGLCNA
RESI BGLCN0
RESI AGALNA
RESI BGALNA
RESI ANE5AC
RESI BNE5AC
RESI ABEQ
RESI ARHMOA
RESI TIP3
RESI MGLYOL
RESI MERYOL
RESI DTHROL
RESI LTHROL
RESI MRIBOL
RESI DARAOL
RESI LARAOL
RESI MXYLOL
RESI MALLOL
RESI DALTOL
RESI LALTOL
RESI DGLUOL
RESI LGLUOL
RESI DMANOL
RESI LMANOL
RESI DGULOL
RESI LGULOL
RESI DIDIOL
RESI LIDIOL
RESI MGALOL
RESI ALLOSE
RESI PSICOS
RESI INI1
RESI INI2
RESI INI3
RESI INI4
RESI INI5
RESI ADEO
RESI BDEO
RESI ARIB
RESI BRIB
RESI AARB
RESI BARB
RESI ALYF
RESI BLYF
RESI AXYF
RESI BXYF
RESI AFRU
RESI BFRU
```

Now I can do a search/replace in VS Code to generate a macro to use for `atomselect`.

Search for `RESI` and replace with `resname`.  
Search for `\n` and replace with `<spcae>` or `<space>`.  
Clean up the beginning and end of selection, and delete the TIP3 (water).

 ```bash
resname AGLC or resname BGLC or resname AALT or resname BALT or resname AALL or resname BALL or resname AGAL or resname BGAL or resname AGUL or resname BGUL or resname AIDO or resname BIDO or resname AMAN or resname BMAN or resname ATAL or resname BTAL or resname AXYL or resname BXYL or resname AFUC or resname BFUC or resname ARHM or resname BRHM or resname AGLCA or resname BGLCA or resname BGLCA0 or resname AIDOA or resname BIDOA or resname AGLCNA or resname BGLCNA or resname BGLCN0 or resname AGALNA or resname BGALNA or resname ANE5AC or resname BNE5AC or resname ABEQ or resname ARHMOA or resname MGLYOL or resname MERYOL or resname DTHROL or resname LTHROL or resname MRIBOL or resname DARAOL or resname LARAOL or resname MXYLOL or resname MALLOL or resname DALTOL or resname LALTOL or resname DGLUOL or resname LGLUOL or resname DMANOL or resname LMANOL or resname DGULOL or resname LGULOL or resname DIDIOL or resname LIDIOL or resname MGALOL or resname ALLOSE or resname PSICOS or resname INI1 or resname INI2 or resname INI3 or resname INI4 or resname INI5 or resname ADEO or resname BDEO or resname ARIB or resname BRIB or resname AARB or resname BARB or resname ALYF or resname BLYF or resname AXYF or resname BXYF or resname AFRU or resname BFRU
```

```py
atomselect macro glycan {
resname AGLC or resname BGLC or resname AALT or resname BALT or resname AALL or resname BALL or resname AGAL or resname BGAL or resname AGUL or resname BGUL or resname AIDO or resname BIDO or resname AMAN or resname BMAN or resname ATAL or resname BTAL or resname AXYL or resname BXYL or resname AFUC or resname BFUC or resname ARHM or resname BRHM or resname AGLCA or resname BGLCA or resname BGLCA0 or resname AIDOA or resname BIDOA or resname AGLCNA or resname BGLCNA or resname BGLCN0 or resname AGALNA or resname BGALNA or resname ANE5AC or resname BNE5AC or resname ABEQ or resname ARHMOA or resname MGLYOL or resname MERYOL or resname DTHROL or resname LTHROL or resname MRIBOL or resname DARAOL or resname LARAOL or resname MXYLOL or resname MALLOL or resname DALTOL or resname LALTOL or resname DGLUOL or resname LGLUOL or resname DMANOL or resname LMANOL or resname DGULOL or resname LGULOL or resname DIDIOL or resname LIDIOL or resname MGALOL or resname ALLOSE or resname PSICOS or resname INI1 or resname INI2 or resname INI3 or resname INI4 or resname INI5 or resname ADEO or resname BDEO or resname ARIB or resname BRIB or resname AARB or resname BARB or resname ALYF or resname BLYF or resname AXYF or resname BXYF or resname AFRU or resname BFRU
}
```

The above macro did not work, but neither did the text below.

```py
atomselect macro lipid2 {
 resname DLPC or resname LPPC or resname DLPE or resname DLPS or resname DLPA or resname DLPG or resname DMPC or resname DMPE or resname DMPS or resname DMPA or resname DMPG or resname DPPC or resname DPPE or resname DPPS or resname DPPA or resname DPPG or resname DSPC or resname DSPE or resname DSPS or resname DSPA or resname DSPG or resname DOPC or resname DOPE or resname DOPS or resname DOPA or resname DOPG or resname POPC or resname POPE or resname POPS or resname POPA or resname POPG or resname SAPC or resname SDPC or resname SOPC or resname DAPC
}
```

There is already a built-in macro for lipid/lipids and for glycans. (So I don't need to make my own macros) for this.

mol modselect 3 0 glycan 
mol modcolor 3 0 ResType


## Resources

## CHEM 181 Introduction to Molecular Simulation

[Introduction to Molecular Dynamics Trajectories](http://copresearch.pacific.edu/mmccallum/181/styled-5/styled-16/index.html): This is done in VMD. Look carefully at the section *Trajectory coloring by structure*. This has useful tips.




