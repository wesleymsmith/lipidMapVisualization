# lipidMapVisualization

This project takes a set of membrane-protein trajectories (after stripping water and ions) and computes and visualizes
various membrane properties.

This is accomplished in several stages.
1) √ extract_membrane_headgroup_centers.ipynb : Extracts lipid headgroup center of mass coordinates
  * Loads the trajectory data using pytraj and computes the center of mass of each phosphate linker group over the
    the trajectory. The resulting arrays are saved in github sized chunks for future use
    ** The needed trajectories for this notebook must be downloaded separately since the required files are larger
       than the github limit and are difficult to break into pieces.
2) √ leaflet_Identification.ipynb: Determines which lipids residues belongs to each leaflet using DBSCAN
  * Check and fix frames for which DBSCAN performs poorly using simple automated anomoly detection
3) (To be added) grid_height_interpolation: Interpolates lipid headgroup heights to a 2D using the scheme found in  equation (S1) of 
  'Doktorova, Milka, et al. "Gramicidin increases lipid flip-flop in symmetric and asymmetric lipid vesicles." 
   Biophysical journal 116.5 (2019): 860-873.'
   * this results in a pair arrays of 2D grids, one array for leaflet, which contain one 2D grid for each
     frame of the trajectory.
   * the 2D grids are regular rectangular lattices with grid spacing of 1 Å
   * also generated are a pair of numpy arrays containing the grid point X and Y coordinates respectively. I.e. as
     generated by the numpy meshgrid function.
   * These are again saved in chunks so that they can be stored directly on github
4) (To be added) grid_density_estimation.ipynb: Compute lipid density as projected over the XY plane using a gaussian kernel density
   estimate.
   * this results in a pair of arrays just as in (3), here, the grid values are the density estimates.
   * the grid setup is identical to that of (3), so the same grid coordinate files can be used.
   * A bandwidth of 2.4 is employed. This corresponds to a radial gaussian smoothing kernel with a sigma of 2.4 Å, which
     is the approximate radius of a phosphate ion.
5) (To be added) visualize_lipid_heights.ipynb: Uses the results of (3) and (4) to view the lipid heights for pairs of systems side by side.
   * The density grids are used to compute a density contour which is overlayed onto the membrane height and thickness
     maps.
   * various widgets are provided to control plotting averages over desired frame ranges and to control the contour level
     for the density mask overlay.
