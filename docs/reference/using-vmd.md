---
title: Using VMD
---

# Using VMD

Download the tutorial files from the [VMD tutorials website](http://www.ks.uiuc.edu/Training/Tutorials/vmd/).

## Common text commands

See the [VMD Text Command Summary](https://www.ks.uiuc.edu/Research/vmd/vmd_help.html#TextCommands)

- `logfile console` to log GUI commands to the `tcl` console
- `exit`: Quit VMD.
- `mol`: Load, modify, or delete a molecule in VMD.
- `logfile`*`filename`*, to log the GUI commands to a file that can be run as a script.
- `mol addrep 0` # adds a representation of molecule 0
- `mol showrep 0 0 off` # turn off molecule 0 (top)
- `logfile off`, to turn off logging.
- `logfile console`, to log the commands to the console when you want to view a GUI command.
- `display resetview`, to reset the view (duh).
- `mol modstyle 0 1 VDW 1.000000 12.000000`
- `mol modstyle 0 1 VDW 0.500000 13.000000`, here 0.5 is the *sphere scale*, and 13 is the *sphere resolution*.
- `mol modstyle 0 1 Tube 0.300000 12.000000`, here 0.3 is the tube *Radius* and 12 is the *resolution*.
- `mol modstyle 0 1 NewCartoon 0.300000 10.000000 4.100000 0`, 
- `mol modcolor 0 1 ResType`, to change coloring to residue type (polar, charged, etc.)
- `mol modselect 0 1 helix`, to select just the helices
- `mol modselect 0 1 (not helix) and (not betasheet)`, to select just the loops
- `mol modselect 0 1 (resname LYS) or (resname GLY)`,
- `mol modselect 0 1 water`,
- `mol modselect 0 1 water and within 3 of protein`, selects all the water molecules that are within a distance of 3 angstroms of the protein
- `axes location off`, turn off the axes in the viewer. See [axes](https://www.ks.uiuc.edu/Research/vmd/current/ug/node123.html) for options.
- `mol modcolor rep_number molecule_number color_method`
- `mol modselect rep_number molecule_number select_method`
- `mol showrep molecule_number rep_number [on | off]`
- `modstyle rep_number molecule_number rep_style:`



## Color

From the [VMD Coloring Methods](https://www.ks.uiuc.edu/Research/vmd/vmd-1.7.1/ug/node72.html) web page:

>There are 1041 colors available in VMD, with color ids ranging from 0 to 1040. The first 17 are, in order:

| Color      | Color ID | Favorite                 |
| ---------- | :------: | :----------------------: |
| blue       | 0        | :octicons-heart-fill-24: |
| red        | 1        |                          |
| gray       | 2        |                          |
| orange     | 3        | :octicons-heart-fill-24: |
| yellow     | 4        | :octicons-heart-fill-24: |
| tan        | 5        |                          |
| silver     | 6        | :octicons-heart-fill-24: |
| green      | 7        |                          |
| white      | 8        | :octicons-heart-fill-24: |
| pink       | 9        | :octicons-heart-fill-24: |
| cyan       | 10       | :octicons-heart-fill-24: |
| purple     | 11       |                          |
| lime       | 12       | :octicons-heart-fill-24: |
| mauve      | 13       | :octicons-heart-fill-24: |
| ochre      | 14       |                          |
| iceblue    | 15       | :octicons-heart-fill-24: |
| black      | 16       |                          |
| yellow2    | 17       | :octicons-heart-fill-24: |
| yellow3    | 18       | :octicons-heart-fill-24: |
| green2     | 19       | :octicons-heart-fill-24: |
| green3     | 20       | :octicons-heart-fill-24: |
| cyan2      | 21       | :octicons-heart-fill-24: |
| cyan3      | 22       | :octicons-heart-fill-24: |
| blue2      | 23       | :octicons-heart-fill-24: |
| blue3      | 24       |                          |
| violet     | 25       |                          |
| 26violet2  | 26       | :octicons-heart-fill-24: |
| magenta    | 27       | :octicons-heart-fill-24: |
| 29magenta2 | 28       | :octicons-heart-fill-24: |
| red2       | 29       |                          |
| red3       | 30       |                          |
| orange2    | 31       | :octicons-heart-fill-24: |
| orange 3   | 32       | :octicons-heart-fill-24: |




### Creating a Selection Macro

This macro will select all the lipids in a trajectory that has a membrane.

```py
atomselect macro lipid {
 resname DLPC or resname LPPC or resname DLPE or resname DLPS or resname DLPA or resname DLPG or resname DMPC or resname DMPE or resname DMPS or resname DMPA or resname DMPG or resname DPPC or resname DPPE or resname DPPS or resname DPPA or resname DPPG or resname DSPC or resname DSPE or resname DSPS or resname DSPA or resname DSPG or resname DOPC or resname DOPE or resname DOPS or resname DOPA or resname DOPG or resname POPC or resname POPE or resname POPS or resname POPA or resname POPG or resname SAPC or resname SDPC or resname SOPC or resname DAPC
}
```

## Using the `atomselect` Command

From [Using the `atomselect` command](https://www.ks.uiuc.edu/Research/vmd/vmd-1.7.1/ug/node181.html)

1. Create a selection given the selection text, molecule id, and optional frame number. The `atomselect` command creates an object, and returns the name of the new atom selection.  
2. Then use the created selection to access the information about the atoms in the selections.

## Creating multiple representations

```py
modstyle rep_number molecule_number rep_method: # use top for molecule number
```

```py
mol modstyle 0 1 NewCartoon 0.300000 10.000000 4.100000 0 # drawing style is new cartoon
mol modselect 0 1 protein # selected atoms are protein
mol modcolor 0 1 Structure # colors by secondary structure
```

```py
mol addrep 1\
mol color ResName\
mol representation VDW 1.000000 12.000000\
mol selection resname LYS\
mol material Opaque
```

```py
mol addrep 0
mol modstyle 4 0 QuickSurf 1.000000 0.500000 1.000000 1.000000
mol modmaterial 4 0 Transparent
mol modcolor 4 0 Molecule
mol color Molecule
mol representation QuickSurf 1.000000 0.500000 1.000000 1.000000
mol selection protein
mol material Transparent
mol modrep 4 0
```

```py
delete molecule_number
```


Be sure that the molecule to load is in the current directory.

```py
source filename.tcl
```

```py
mol new 1ubq.pdb
mol modstyle 0 1 NewCartoon 0.300000 10.000000 4.100000 0
```

`set` *`variable`* *`value`*  
*`$variable`* refers to the value of *`variable`*.  
Use the shortcut `top` to refer to the top molecule instead of a molecule ID.

## Selecting Lipids

Download and install the [membplugin](https://sourceforge.net/projects/membplugin/)

```py
resname POPC and name "C[23].*" and not name "C[123]"
```



From [this site](https://www.ks.uiuc.edu/Research/vmd/mailing_list/vmd-l/29266.html)

```py
name N "C1[1-5]" "H1[1-5]." P "O1[1-4]" # Headgroup only
name "C[1-3]" "H." "C[2-3]1" "O[2-3][1-2]" # glycerol + carbonyl
name "H.*[R-Z]" "C[2-3][2-9]" "C[2-3]1." # Acyl chain
```

Although in Tcl scripts, the braces and double quotes need to be escaped so that the interpreter doesn't think they are a command. Ex:

```py
set sel [atomselect top "name \"H.*\[R-Z\]\" \"C\[2-3\]\[2-9\]\" \"C\[2-3\]1.\""]
```

The `atomselect` command creates an object. 

## Setting up VMD

### the `.vmdrc` file

type `menu list` in the Terminal window to get the list of names for the various menus.
The `tkcon menu on` trick I got from the [VMD mailing list](the `tkcon` menu trick I got from [here](https://www.ks.uiuc.edu/Research/vmd/mailing_list/vmd-l/19823.html)

```bash
# position and turn on menus
menu main on
after idle {
  after 2 {
    menu tkcon on
  }
}

# change directory
cd ~/vmd-work
```

## Top molecule

By default the last molecule loaded in the VMD is the top molecule.  
There can be only one top molecule at a time.  
The top molecule is indicated by a T flag in the VMD Main window.  
The top molecule is the default molecule for mol commands when nothing is specified.

## Change Background Color

```py
color Display Background white
```

## Color

`change rgb color`*`r g b`*: Set rgb of *color* to *r g b*.

rgb values have to be decimals.

From Pymol (divide by 255):

```py
set_color blueC= [20, 108, 150] # 0.078431 0.423529 0.588235
set_color blueN= [4, 64, 93] #    0.015686 0.25098 0.364706
set_color blueO= [10, 83, 118] #  0.039216 0.32549 0.462745
set_color blueH= [83, 147, 178] # 0.28819 0.57647 0.69804
set_color blueS= [50, 122, 156] # 0.1961 0.47843 0.611765
```

From the [vmd wiki](https://www.ks.uiuc.edu/Research/vmd/mailing_list/vmd-l/4880.html)

- See the vmd users manual to use a script to assign specific RGB colors to specific color scale values.
- Set the color scale data range to 0 to 1023.
- Then whatever beta/user value you assign to an atom will correspond directly to the color you want.
- Now you have 1024 colors you can assign any way you like.

Script

```py
proc setcolorscaleindex { index r g b } {
  set colorindex [expr [colorinfo num] + $index]
  color change rgb $colorindex $r $g $b
}
setcolorscaleindex 0 1 1 1
setcolorscaleindex 1 1 0 0
setcolorscaleindex 2 0 1 0
setcolorscaleindex 3 0 0 1
setcolorscaleindex 4 0 1 1
setcolorscaleindex 5 1 0 1
setcolorscaleindex 6 1 1 0
set sel [atomselect top all]
$sel set beta 0.0 # this sets the beta value for all atoms to 0
$sel delete # delete the selection "sel"
set sel [atomselect top "name CA"] # create a new selection, "sel", that contains the alpha carbons
$sel set beta 1.0 # set the beta value for the alpha carbons to 1.0
$sel delete # delete the selection
mol modcolor 0 0 Beta # use the beta coloring scheme to color the molecule
## note that the 'mol scaleminmax' command has to be last...
mol scaleminmax 0 0 0 1023
```

```py
color change rgb $colorindex $r $g $b

color change rgb 40 0.078431 0.423529 0.588235
color change rgb 41 0.015686 0.25098 0.364706
color change rgb 42 0.039216 0.32549 0.462745
color change rgb 43 0.28819 0.57647 0.69804
color change rgb 44 0.28819 0.57647 0.69804
color change rgb 45 0.1961 0.47843 0.611765
```

```py
$sel set beta 40
mol modstyle 0 0 vdw
```

```py
set sel [atomselect top "hydrophobic"] # This creates a selection containing all the hydrophobic residues.
$sel set beta 1 # label all hydrophobic atoms by setting their beta values to 1.
```

[Paletton.com](https://paletton.com/#uid=1000u0kllllaFw0g0qFqFg0w0aF)

### Materials

See the [VMD Materials wiki page](https://www.ks.uiuc.edu/Research/vmd/current/ug/node88.html).

## Modifying a Selection

---

```py
cd 1-tutorials
mol new 1ubq.pdb # loaded as molecule 0
```

```py
setcolorscaleindex 40 0.078431 0.423529 0.588235
setcolorscaleindex 41 0.015686 0.25098 0.364706
setcolorscaleindex 42 0.039216 0.32549 0.462745
setcolorscaleindex 43 0.28819 0.57647 0.69804
setcolorscaleindex 44 0.28819 0.57647 0.69804
setcolorscaleindex 45 0.1961 0.47843 0.611765
```

---

another attempt at beta coloring

```py
set crystal [atomselect top "all"]
$crystal set beta 0
set sel [atomselect top "hydrophobic"]
$sel set beta 1
$crystal set radius 1.0
$sel set radius 1.5 
```

[Changing the color scale definitions](https://www.ks.uiuc.edu/Research/vmd/vmd-1.8.3/ug/node183.html)

```py
proc tricolor_scale {} {
  set color_start [colorinfo num]
  display update off
  for {set i 0} {$i < 1024} {incr i} {
    if {$i == 0} {
      set r 1;  set g 0;  set b 0
    }
    if {$i == 511} {
      set r 1;  set g 1;  set b 1
    }
    if {$i == 513} {
      set r 0;  set g 0;  set b 1
    }
    color change rgb [expr $i + $color_start     ] $r $g $b
  }
  display update on
}

tricolor_scale
```

---

Once the beta values for atoms have been changed, they stay changed. You can then assign a color to a beta value, and then choose the coloring method "beta" to assign the color to a beta value. 

This worked:

```py
proc setcolorscaleindex { index r g b } {
  set colorindex [expr [colorinfo num] + $index]
  color change rgb $colorindex $r $g $b
}
>Main< (1-tutorials) 90 % 
>Main< (1-tutorials) 90 % setcolorscaleindex 0 1 1 1
>Main< (1-tutorials) 91 % setcolorscaleindex 1 1 0 0
>Main< (1-tutorials) 92 % setcolorscaleindex 2 0 1 0
>Main< (1-tutorials) 93 % setcolorscaleindex 3 0 0 1
>Main< (1-tutorials) 94 % setcolorscaleindex 4 0 1 1
>Main< (1-tutorials) 95 % setcolorscaleindex 5 1 0 1
>Main< (1-tutorials) 96 % setcolorscaleindex 6 1 1 0
>Main< (1-tutorials) 97 % set sel [atomselect top all]
atomselect6
>Main< (1-tutorials) 98 % $sel set beta 4
>Main< (1-tutorials) 99 % $sel set beta 0.0
>Main< (1-tutorials) 100 % $sel set beta 3
>Main< (1-tutorials) 101 % $sel set beta 2
>Main< (1-tutorials) 102 % $sel set beta 6
>Main< (1-tutorials) 103 % mol modcolor 0 0 Beta
>Main< (1-tutorials) 104 % mol scaleminmax 0 0 0 1023
>Main< (1-tutorials) 105 % mol scaleminmax 0 0 0 1023
>Main< (1-tutorials) 106 % $sel set beta 4
>Main< (1-tutorials) 107 % $sel set beta 3
>Main< (1-tutorials) 108 % $sel set beta 2
>Main< (1-tutorials) 109 % $sel set beta 1
>Main< (1-tutorials) 110 % $sel set beta 5
>Main< (1-tutorials) 111 % $sel set beta 6
>Main< (1-tutorials) 112 % setcolorscaleindex 0 0.078431 0.423529 0.588235
>Main< (1-tutorials) 113 % setcolorscaleindex 6 0.1961 0.47843 0.611765
>Main< (1-tutorials) 114 % mol scaleminmax 0 0 0 1023
>Main< (1-tutorials) 115 % $sel set beta 0
>Main< (1-tutorials) 116 % $sel set beta 1
>Main< (1-tutorials) 117 % setcolorscaleindex 43 0.28819 0.57647 0.69804
>Main< (1-tutorials) 118 % mol scaleminmax 0 0 0 1023
>Main< (1-tutorials) 119 % $sel set beta 43
>Main< (1-tutorials) 120 % $sel set beta 42
>Main< (1-tutorials) 121 % 
```

Remember to use `logfile <filename>` to log commands to a file that you can turn into a script. 

---

## VMD and NAMD tutorials

[quickMD tutorial](http://www.ks.uiuc.edu/Training/Tutorials/qwikmd/qwikmd-tutorial.pdf)  
[Tutorial: A quick MD simulation using NAMD and VMD](https://bioinformaticsreview.com/20200619/a-quick-md-simulation-using-namd-and-vmd/)  
[HPRC Short Course: Classical Molecular Dynamics with NAMD](https://hprc.tamu.edu/files/training/2021/Spring/HPRC-Classical-NAMD-tutorial.pdf)  

## Scripting in VMD

This was taken from the [Scripting in VMD](https://www.ks.uiuc.edu/Training/Tutorials/vmd/tutorial-html/node4.html) web page.

### Quick tutorial

- Start a VMD session.
- Select *Extensions → Tk Console*.
- Download `1ubq.pdb` and move it to the `vmd-work` directory.
- Change to the `vmd-work` directory using the console.
- Type `mol new 1ubq.pdb` and click enter.
- Type `set crystal [atomselect top "all"]` in the *TkConsole* window.

This creates a `crystal` selection that we can do stuff with.

- Type `$crystal num` in the *Tk Console window*.

## Movie making

Purpose: to make a video illustration of a MD simulation of the Covid-19 spike protein in a membrane that I can use for teaching. This is also a nice exercise for learning VMD.

Here is a nice short tutorial on [Movie Making from molecular dynamics simulation with VMD](https://www.youtube.com/watch?v=lueqjpjo3yY), most importantly, use the *trajectory smoothing* function.

![type:video](https://www.youtube.com/embed/lueqjpjo3yY)

There is a nice VMD function for [Tracking Script Command Versions of the GUI Actions](http://www.ks.uiuc.edu/Research/vmd/current/ug/node24.html). 

I can go through a bunch of tutorials and then use the script commands.

[visualizing glycans in protein structures](http://glycam.org/docs/help/2015/10/02/visualizing-pdb-files-containing-glycans/)

### Random Notes

I found a [Covid-19 spike protein trajectory](https://charmm-gui.org/?doc=archive&lib=covid19) on the [CHARMM-GUI](https://charmm-gui.org/) website.

[ambient occlusion lighting with tachyon](http://www.ks.uiuc.edu/Research/vmd/minitutorials/tachyonao/)

Need to learn:

- how to select the different parts of the molecules
- how to make a movie from the trajectory

A good place to start is the [VMD User's Guide](http://www.ks.uiuc.edu/Research/vmd/current/ug/ug.html).

## Saving an Image


