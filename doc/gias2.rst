*****
GIAS2
*****

`GIAS2 <https://bitbucket.org/jangle/gias2>`_ is a free and open-source Python library used by most MAP Client plugins written by Ju Zhang. It has a wide range of functionalities aimed at musculoskeletal modelling. This page provides some background on GIAS2 and looks at some of its parts which may be useful for extending current and writting new MAP Client plugins.

Background
==========

GIAS2 has grown organically with the developement of the MAP Client and its plugins. It has served as library for storing functions and classes commonly used by many plugins and projects of mine outside of MAP. It's functionalities can be broadly categoried into:

- Geometric transformations
- Rigid and non-rigid Registration
- Image segmentation (active shape models and random forest regression)
- Mesh processing
- Statistical shape models
- Lower-limb bone models

GIAS2 makes heavy use of the SciPy and NumPy. In addition, certain sub-packages depend on PyDicom, Scikit-Learn, Matplotlib, and Mayavi (for 3D visualisation). GIAS2 is licensed under the Mozilla Public License Version 2.0.

Having grown organically, GIAS2 does suffer from issues such as lack of documentation, in-complete features in some areas, and can probably do with some refactoring. It does have a collection of example scripts which demonstration the usage of some of its features. The MAP Client plugins on which it depends provide some more examples. The rest of this page will look at some functions and classes commonly used by those plugins. 

Registration
============

Fieldwork
=========

Musculoskeletal
===============