# Coulombic-LJ

### Initialization Parameters
- Constant $nVT$ ensemble
  - $n=27000$
  - $T=0.8$
- Polyer beads (30 per chain) uniformly at constant charge of $q_p=-1$
- Univalent counterions
- LJ-potential $\varepsilon=5.0$

### System Variables
- Uniform 19-bead disk-shaped filler bead charge $q=q_f$
- Filler concentration $f=\{25,50,75,100\}$

### Output Parameters
- Stress Autocorrelation function (SAF) $G(t)$
- Step Strain test (SST) $S(t)$
- Radial distribution function (RDF) 
- Newtork clustering algorithm (NCA)
  - Asphericity $\alpha_s$
  - Acylindricity $\alpha_c$
  - Relative shape anisotropy $\kappa^2$
  
# How to Run

1. Copy the contents of the `package` folder into each restart folder.
2. Copy the contents of the `package_allF` folder into an `all_concentrations` folder for each charge.

### Network Clustering Algorithm (NCA)
1. Move the files `chains_after.lammpstrj` and `filler_after.lammpstrj` into the `NCA` folder.
2. Set the `N_FILLER` variable in `sheet_clusterV1.1.c` to the according number of filler particles.
3. Open terminal in the `NCA` folder and run the command `gcc sheet_clusterV1.1.c -o sheet_clusterV1.1 -lm`.
4. Run the command `./sheet_clusterV1.1`.

### Radial Distribution Function (RDF)
1. Move the five `tmp.....rdf` files into the `RDF` folder.
2. Set the file `data` to `tmpX_Y.rdf` and the file `output` to `tmpX_Y.txt` in `RDF.c`.
3. Run `RDF.c` for each pair of atom types `X` and `Y`.

### Stress Autocorrelation Function (SAF)
1. Move the file `Sauto.DAT` into the `SAF` folder.
2. Run `Gt.c` setting temperature to be `0.8` and the volume to be the value from `log.lammps`.
3. Combine the `str_cor_long.txt` data for all four filler concentrations into one file `qX_aggregate.txt` for the specified charge `X`.
4. Set the file `in` to `qX_aggregate.txt` and `out` to `qX_Gt_avg.txt` in `Average_Gt.c`.
5. Run `Average_Gt.c` and plot the resulting data on a logarithmic time scale. (Remember to delete the last line of `qX_Gt_avg.txt`.)

### Step Strain Test (SST)
1. Move the file `stress.out` into the `SST` folder.
2. Set the absolute paths of the `stress.out` input files and `stressXf.txt` output files for all filler concentrations `X`.
3. Run `unzip_stress_files.ipynb`.
4. Combine the `stressXf.txt` data for all four filler concentrations `X` into one file `qY_stress.txt` for the specified charge `Y`.
5. Set the file `in` to `qY_stress.txt` and `out` to `qY_St_avg.txt` in `AvgSt.c`.
6. Run `AvgSt.c` and plot the resulting data on a logarithmic time scale. (Remember to delete the last line of `qY_St_avg.txt`.)
