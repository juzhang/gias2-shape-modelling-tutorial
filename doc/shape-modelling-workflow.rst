************************
Shape Modelling Workflow
************************

This tutorial will use GIAS2 tools to processes a set of meshes, e.g. segmented femurs, to generate a mean mesh and principal components of shape variation.

[shape modelling background]

The workflow is composed of running three commandline scripts:

1. :code:`gias-rbfreg`: Non-rigid registration of a reference mesh to all training meshes
2. :code:`gias-rigidreg`: Rigid-body registration to align all fitted meshes to the reference mesh
3. :code:`gias-trainpcashapemodel`: Perform PCA on the aligned meshes to calculate the mean mesh and principal components of shape variation.

Data Organisation
====================
Each of the gias scripts will read in a set of meshes and output a set of meshes. Let's take a look at the input/output file directories prepared for this tutorial. In the data/ directory, we have

- `segmentations/`: Segmented meshes for input to :code:`gias-rbfreg`. In this tutorial, these are 10 femurs segemented from the Melbourne Femur Collection [cite].
- `fitted_meshes/`: Fitted meshes output by `gias-rbfreg`, used as input for :code:`gias-rigidreg`.
- `aligned_meshes/`: Aligned meshes output by `gias-rigidreg`, used as input for :code:`gias-trainpcashapemodel`.
- `shape_model/`: Shape model outputs by :code:`gias-trainpcashapemodel`.

Each script takes as argument a text file containing the file paths of its input meshes. These text files are in the `data/` directory:

- `rbfreg_list.txt`: Segmented meshes for input into :code:`gias-rbfreg`.
- `rigidreg_list.txt`: Fitted meshes for input into :code:`gias-rigidreg`.
- `pca_list.txt`: Aligned meshes for input into :code:`gias-trainpcashapemodel`.

0. Getting Started
==================
Open a terminal (on windows, an Anaconda prompt), and navigate to the tutorial `data/` directory. This is the folder where the `rbfreg_list.txt` etc files are.

1. Mesh Fitting
===============
The first step of the workflow is to non-rigidly register or fit one of our segmentations to the other segmentations, thereby representing all our segmentations by correspondent meshes. We run::

        gias-rbfreg -b rbfreg_list.txt -d fitted_meshes --outext .ply

Let's look at each argument of the command above:

- :code:`-b rbfreg_list.txt`: invokes batch mode for `gias-rbfreg` and gives it the list of meshes to morph. `gias-rbfreg` will use the FIRST mesh in the list as the reference to morph to all other meshes in the list.
- :code:`-d fitted_meshes`: defines the directory fitted meshes will be written into. "_rbfreg" will be appended to the end of the input file names.
- :code:`--outext .ply`: defines the output file format. In this case, we define fitted meshes to be in the PLY format.

Run :code:`gias-rbfreg --help` to see the full list of commandline arguments.

As the script runs, you will see output .ply mesh files appear in the `data/fitted_meshes` folder.

2. Rigid Alignment
==================
The second step of the workflow is to rigidly align the fitted meshes to remove rotational and translational variations. We run::
    
    gias-rigidreg corr_r -b rigidreg_list.txt -d aligned_meshes --outext .ply

The argument :code:`corr_r` tells gias-rigidreg to use the correspondent rigid registration mode. If we want to normalise size as well, we can use :code:`corr_rs` to apply scaling during alignment As is step 1, the other arguments define the list of meshes to process, the output directory, and the output file format. "_rigidreg" will be appended to the end of input filenames.

Run :code:`gias-rigidreg --help` to see the full list of commandline arguments.

As the script runs, you will see output .ply mesh files appear in the `data/aligned_meshes` folder.

3. PCA
======
The final step of the workflow is to perform PCA on the aligned meshes to generate our mean mesh and principal components. In additional, we will also generate meshes along each of the first 3 principal components. We run::

    gias-trainpcashapemodel pca_list.txt -n 10 -r 0 1 2 -o shape_model/femur --plot_pcs 10 -v

In the command above

- :code:`pca_input.txt`: defines the file containing the list of aligned meshes to process
- :code:`-n 10`: tells the script to calculates the first 10 principal components using an incremental PCA method [cite]. If we leave this argument out, the script will attempt to calculate all principal components, which may result in memory errors if the number of features is greater than ~10,000.
- :code:`-r 0 1 2`: tells the script to reconstructs meshes at +2 and -2 standard deviations along the first 3 principal components (number starts at 0).
- :code:`-o shape_model/femur`: defines the output file name. Reconstructed meshes will have this as the first part of their filenames.
- :code:`--plot_pcs 10`: tells the script to display plots of the variance explained by each of the first 10 principal components and the spread of our shapes in shape space. Make sure the number given here is equal or less than the number of principal components to calculate.
- :code:`-v`: turns on 3D visualisation of the meshes and principal components (mayavi must be working for this to work).

Run :code:`gias-trainpcashapemodel --help` to see the full list of commandline arguments.

As the script runs, you will see the mean and reconstructed meshes appear in the shape_models folder. There is also the femur.pc.npz file which contains the principal component vectors and scores. This file can be loaded using `numpy.load`. 

Two figures will also appear. The bar graph shows the proportion of variance explained by each principal component. The scatter-plot shows the spread of each meshes principal component score along the first two principal components.

Once you close these two plot windows, the 3-D model viewer will appear if Mayavi is installed and working.

1. To show the mean mesh, select "mean" in the "tri surfaces" combobox and click "update" below the combobox. The mesh should appear in the interactive scene on the right of the window.
2. To interactively change the shape of the mesh along principal components, switch to the "statistical shape model" tab. Select "principal components" in the "PC Model" combobox, select "mean::tri" in the "PC Geometry" combobox.
3. In the "Mode index" field, select the principal component, then drag the slider below to deform the mesh along the selected principal component.
