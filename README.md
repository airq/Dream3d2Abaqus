[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3665452.svg)](https://doi.org/10.5281/zenodo.3665452)
# Dream3d2Abaqus
## Main Function
Convert microstructure information generated by Dream3d (opensource software which can be used to synthetically build different microstructure which can be found [here](http://dream3d.bluequartz.net/)) to construct an Abaqus input file.

The generated microstructure features and orientations are assigned to element sets in Abaqus with the corresponding material definition assigned via sections.

In addition, files *node_coordx.txt*, *node_coordy.txt*, and *node_coordz.txt* are created which contains the nodes of each feature and the corresponding features that the node is shared with.
## Dream3D Requirements
The minimum filter construction required is as follows:

<img src="/Images/dream3d_filters.png" width="250" height="400">

Centroid information will be stored in the *csv* file (created using the *Export Feature Data as CSV File* filter), while node/element/orientation information is stored in the *.vox* file (created using the *Export Los Alamos FFT File* filter).

Information required to understand the distance from the grain boundary is provided by the filter *Find Euclidean Distance Map*.  This should be exported with the corresponding FeatureIds using the *Export ASCII Data* filter and then added to the same file with the first column corresponding to the distance and second column the featureid.
## Required informtion for Matlab function
To use the Matlab function, the *xlsx* file included here should be updated with the material parameters in the sheet (with the corresponding name) in the order provided in the pdf found [here](http://www.columbia.edu/~jk2079/Kysar_Research_Laboratory/Single_Crystal_UMAT.html). 

The location of the centroid of each grain can be extracted from the generated *csv* file.  These values should be transferred to the *centroid* sheet in the *xlsx* file (inputfile_info)

## Installation
Simply copy files in the folder titled *Dream3d2Abaqus* into the MATLAB file path.

## Running the MATLAB function
Run from the command prompt the following:
*dream2abq2('gbvoxfile.vox','nameofvoxfile.vox','nameofinputfile.inp')*
where:
* nameofvoxfile = name of the vox file included in the same directly and which is exported using the *Export Los Alamos FFT File* filter
* nameofinpfule = is the name of the Abaqus input file you would like to create
* gbvoxfile = the vox file which contains the distance to the grain boundary and the corresponding featureId extracted from Dream3D
