.. _qstart:

==============
Quickstart
==============

-------------------
Directory structure
-------------------

Here’s a brief description of each top-level directory:

.. topic:: /core

   contains the Nek5000 application sources.

.. topic:: /mycases

   consistent place for users to place their problem cases.

.. topic:: /examples

   contains example problems. Note: NOT included in the master branch on the GitHub repo.

---------------------
Case files
---------------------

.. topic::  SIZE

   contains some hardwired runtime parameters to dimension static arrays.

.. topic::  foo.par

   contains runtime parameters.

.. topic::  foo.re2

   contains mesh and boundary data.

.. topic::  foo.ma2

   contains partioning data.

.. topic::  foo.usr

   contains user specific code to initialize solver, set source terms and boundary conditions or to manipulate solver internals.

.. topic::  foo.his

   contains probing points.
 
.. topic::  foo.f00000

   contains checkpoint data.

.. topic::  foo.nek5000

   contains metadata for VisIt or ParaView.

-------------------
Scripts
-------------------

Let’s walk through some useful batch scripts:

- ``makenek <case>`` compiles your case
- ``nek/nekb <case>`` runs a serial job in foreground or background
- ``nekmpi/nekbmpi <case> <number of ranks>`` runs a parallel job
- ``neknek <case1> <cas2> <ranks 1> <ranks 2>`` runs Nek5000 with two overlapping component grids 
- ``visnek <case>`` creates metadata file required by `VisIt <https://wci.llnl.gov/simulation/computer-codes/visit/>`_ and `ParaView <https://www.paraview.org/>`_. 
- ``mvn <old name> <new name>`` renames all case files
- ``cpn <old name> <new name>`` copies all case files

----------------------------------
Running your very first simulation
----------------------------------

Hold your horses, this needs less than 5 min.  
Begin by downloading the latest release tarball from `here <https://github.com/Nek5000/Nek5000/releases>`_.
Then follow the instructions below

::

  cd ~
  tar -xvzf Nek5000_X.Y.tar.gz
  export PATH=$HOME/Nek5000/bin:$PATH
  cd ~/Nek5000/tools; ./maketools genmap
  cd ~/Nek5000/run
  cp -r ../examples/eddy_uv .
  cd eddy_uv
  genmap                       # run partioner, on input type eddy_uv 
  makenek eddy_uv              # build case, edit script to change settings
  nekbmpi eddy_uv 2            # run Nek5000 on 2 ranks in the background
  tail logfile                 # view solver output
  visnek eddy_uv; visit -o eddy_uv.nek5000 # requires a VisIt/Paraview installation

