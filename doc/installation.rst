***********************
GIAS2 Installation
***********************

Windows - Python 2 Anaconda Environment
=======================================

Anaconda is an umbrella package of Python packages for scientific computing. It is a convenient way to set up a Python environment with the dependencies for MAP Client and its plugins.

1. Install `Anaconda <https://www.continuum.io/downloads>`_ for Python 2.7
2. Install GIAS2 dependencies in the Anaconda environment
    
    2.1. Open a Anaconda 2 command prompt: Start > All programs > Anaconda2 > Anaconda Prompt
    
    2.2. Install Git and Mayavi via the commandline::
        
        conda install mayavi scipy matplotlib

    Enter "y" for questions confirming the install, e.g. having to downgrade some packages.

3. Download the `latest GIAS2 release <https://bitbucket.org/jangle/gias2/downloads>`_ in the whl format.
4. Install GIAS2 via the commandline prompt::

        pip install path\to\gias2-X.X.X-py2-none-any.whl

where X.X.X is the version number.

5. You now should be able to import gias2 in a python session::
    
    python
    import gias2

Linux, Python 2 
===============
1. Install dependencies

    apt-get install mayavi2 pip

2. Download the `latest GIAS2 release <https://bitbucket.org/jangle/gias2/downloads>`_ in the whl format.
3. Install GIAS2 via the commandline prompt::

        pip install path\to\gias2-X.X.X-py2-none-any.whl

where X.X.X is the version number.

4. You now should be able to import gias2 in a python session::
    
    python
    import gias2

Linux, Python 3 (Not Recommended)
=================================

Note that you are likely to suffer problems with Mayavi in Python 3. As a result, 3-D visualisation will not work for gias-trainpcashapemodel.

1. Build and install VTK and VTK python bindings. `This <http://ghoshbishakh.github.io/blog/blogpost/2016/07/13/building-vtk-with-python3-wrappers.html>`_ is a good tutorial.

2. Install visualisation dependencies

    pip install mayavi matplotlib

3. Download the `latest GIAS2 release <https://bitbucket.org/jangle/gias2/downloads>`_ in the whl format.
4. Install GIAS2 via the commandline prompt::

        pip install path\to\gias2-X.X.X-py3-none-any.whl

where X.X.X is the version number.

5. You now should be able to import gias2 in a python session::
    
    python
    import gias2
    