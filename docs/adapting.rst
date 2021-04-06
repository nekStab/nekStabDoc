
Adapting your case
==================

git update-index --chmod +x script.sh

we recommend converting old *.rea* files to **.par** + **.re2** and
**.ma2**

in *SIZE* be sure to modify and include:

.. code:: fortran

    parameter (lpelt=lelt)
    include 'NEKSTAB.inc'

in your *.usr*, add to **userchk** and **userf **\ respectively:

::

    call nekStab
    call nekStab_forcing(ffx,ffy,ffz,ix,iy,iz,ieg)

Programming best practices
==========================

    The best style is consistent style!

#. Always use **implicit none** with exception from *.usr*
#. Comments with ! instead of c
#. Use tab length with 3 space characters
#. small caps for fortran syntax : while, for, do, etc.
#. proper define real numbers: 0.0d0, 0.50d0, 1.0d0
#. subroutine -> return, end
#. to print output we use write(6,\*)
#. stop the code with *call **exitt***
#. use *nelv* instead of **nelt** for consistency as we must respect
   velocity mesh
#. use *n* and *n2* for loops instead of *ntot1*
#. local field declarations with *lt* and *lt2*

.. code:: fortran

    real, save, intent(inout), dimension(lt) :: field1,field2,field3

#. shared variables in our custom x\_SIZE.f respecting the standard Nek
   style like in /core

.. code:: fortran

    c     Solution data
          real vx     (lx1,ly1,lz1,lelv)
         $    ,vy     (lx1,ly1,lz1,lelv)
         $    ,vz     (lx1,ly1,lz1,lelv)
          common /vptsol/ vx, vy, vz

#. Limit line length increased to 132 to avoid excessive use of
   continuation tabs, in most cases we are slightly over the 72
   characters standard

.. |Build Status| image:: https://travis-ci.com/ricardofrantz/nekStab.svg?token=DpocmcBgXShNTZ9nAQ5y&branch=master
   :target: https://travis-ci.com/ricardofrantz/nekStab