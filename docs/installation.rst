INSTALLING AND RUNNING
======================

Fist install code dependencies if running with GCC

.. code:: bash

    sudo apt-get -y install libmpich-dev mpich libopenblas-dev build-essential cmake m4

Clone the repository and Nek5000 as a submodule:

.. code:: bash

    git clone --depth=50 --branch=master https://github.com/ricardofrantz/nekStab.git
    cd nekStab
    git submodule update --init --recursive

Run **(sudo) vim $HOME/.bashrc** and add the following:

.. code:: bash

    export NEKSTAB_SOURCE_ROOT=$HOME/nekStab
    export NEK_SOURCE_ROOT=$NEKSTAB_SOURCE_ROOT/Nek5000
    export PATH=$NEK_SOURCE_ROOT/bin:$PATH

Compile Nek5000 tools:

.. code:: bash

    cd ~/nekStab/Nek5000/tools
    ./maketools all

| 
|  Outputs

| ``javascript building genmap ... done building gencon ... done building genbox ... done building n2to3 ... done building reatore2 ... done building nekmerge ... done building prenek ... done building postnek ... done building nekamg_setup ... done building gmsh2nek ... done building exo2nek ... done building cgns2nek ... done``
| 

Move to a specific example, for instance: **cd examples/1cyl**

.. code:: bash

    ./cmpile.sh all
    nekbmpi 1cyl 4
