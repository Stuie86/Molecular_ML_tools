# Molecular_ML_tools
Tools used in the development of the worlds first fully Machine Learned molecular dynamics forcefield, FFLUX. 

# Programs included are:
-  DensityNodes
-  GetStats
-  FeatureOrder


---------------------------------------------------------------------------------------
DensityNodes
---------------------------------------------------------------------------------------
Fortran90 program to position nodes at locations of high water density around a solvate molecule. Reads in training set file (coordinates of system in spherical coordinates), and requires the solvating molecules to be listed after the solvent. Outputs: file 'node_carts.txt' that lists nodes as Helium atoms in xyz file format; file 'node_feats.txt' that lists nodes as features to be used by other programs.

To run this program you need one training set file (a list of molecular configurations in spherical coordinates) of a solvated system, where all the water molecules are listed after the solute. The program will prompt for the number of solute atoms, the number of water molecules, resolution, overlap, and number of nodes.

To calculate density, the volume of the molecule is partitioned into a 3d grid. Resolution is the length of one side of one grid cell, in Angstroms (expected input is in Bohr), overlap is is the number of surrounding cells that have their count added. The weight of the surrounding cells decreases linearly.

Written as a single file, self contained program to make it easier to copy/edit/compile/run.

---------------------------------------------------------------------------------------
GetStats
---------------------------------------------------------------------------------------
Takes file of predictions and true values and calculates various prediction metrics. Set up for either output of Popelier group program FEREBUS, or text file in the format shown below. For FEREBUS option, must have FINPUT.txt file and FEREBUS prediction files in current directory. For text file option, values must start on first line of file.

example_input.txt: True_value_1 Predicted_value_1 True_value_2 Predicted_value_2 True_value_3 Predicted_value_3 . . . True_value_n Predicted_value_n

---------------------------------------------------------------------------------------
FeatureOrder
---------------------------------------------------------------------------------------
Orders training set features (in spherical polar coordinates) based on distance from nodes, or the atom of interest in the absence of a node list. Can also strip water molecules from training set file. Input required is one training set (list of molecular configurations in spherical polar coordinates, plus 25 properties, an error and a counter. Everything after configurations can be substituted by 27 0's), with water molecules listed after solute molecules. Program will prompt for file name, number of solute atoms, number of water molecules,and number of molecules to strip from file.

If no 'node_feats.txt' file is present, will acts as if all nodes are centered at the origin (i.e. the atom of interest), and will output an example 'node_feats.txt' file. Otherwise, features will be read from 'node_feats.txt'. Any nodes not listed in 'node_feats.txt' will be positioned at the origin.

