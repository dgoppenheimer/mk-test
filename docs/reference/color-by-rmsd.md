---
title: Coloring by RMSD
---

# Coloring by RMSD in VMD

A nice script to color residues by RMSD

From the [VMD-L Mailing List](https://www.ks.uiuc.edu/Research/vmd/mailing_list/vmd-l/19545.html)

Coloring of residues by rmsd

> This could certainly be done. You would just need to measure
> the RMSD values for each residue, and then store the results into
> one of the available per-atom data fields for each atom in the residue
> (e.g. use a "same residue as ...." type atom selection.)
> Once the data has been stored, you can use the field you've loaded the
> RMSD values into as the coloring method in VMD. For a time-varying
> property, like RMSD or RMSF you'll want to use one of the four "user" 
> fields, since they are stored per-atom, for each frame.


ngmx -s /Volumes/Files-01/Molec\ Dynamics/covid-spike-6vxx_1_1_1_traj_dcd/trj_nos.dcd

/Volumes/Files-01/Molec\ Dynamics/charmm-gui-8939678077/gromacs/topol.top


ngmx -s topol.tpr -f traj.xtc