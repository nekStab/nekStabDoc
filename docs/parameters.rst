Parameters 
==========

Current form of input via uparams 
--------------------------------- 

-  uparam(1) = mode (0: DNS, 1:stabilization, 3:stability)

-  uparam(2) = optional restart vector for stability

-  uparam(3) = stabilzation technique (1:SFD)

-  uparam(4) = frequency cuttor of forcing frequency

-  uparam(5) = gain or forcing amplitude

-  uparam(6) =

-  uparam(7) =

-  uparam(8) =

-  uparam(9) =

-  uparam(10): sponge strenght (>0 to activate)


uparam(1) = 0 - > Direct numerical simulation

uparam(1) = 3.- > Direct mode computation

uparam(1) = 3.2 - > Adjoint mode computation

uparam(1) = 3.3 - > Direct-adjoint mode computation for transient growth
analysis


Future update via parser 
------------------------ 


-----------------------------------
Parameter File (.par)
-----------------------------------

.. Converged Eigenvalues: 2 
   Magnitude   Angle   Growth  Frequency
   EV: 0 1.00112 0.124946 0.0022353 0.249892
   Writing: "Channel-al_eig_0.fld"
   EV: 1 1.00112 -0.124946 0.0022353  0.249892
   Writing: "Channel-al_eig_1.fld"

.. _tab:stabparams:

.. table:: ``STABILITY`` keys in the ``.par`` file

   +-------------------------+------------------------+---------------------------------------+
   | | Key                   | | Value(s)             | | Description                         |
   +=========================+========================+=======================================+
   | ``eigenSolver``         | | ``(none)``           | | Eigenvalue solver                   |
   |                         | | ``arnoldi``          |                                       |
   |                         | | ``Krylov-Schur``     |                                       |
   |                         | | ``custom``           |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``evolOperator``        | | ``(direct)``         | | Evolution operator                  |
   |                         | | ``adjoint``          |                                       |
   |                         | | ``transientGrowth``  |                                       |
   |                         | | ``optimalFrequency`` |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``baseFlow``            | | ``(steady)``         | | Base flow information               |
   |                         | | ``mean``             |                                       |
   |                         | | ``periodic``         |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``krylovDimension``     | | ``<int>``            | | Krylov-space dimension              |
   +-------------------------+------------------------+---------------------------------------+
   | ``SchurTarget``         | | ``<int>``            | | Convergence target for Krylov-Schur |
   +-------------------------+------------------------+---------------------------------------+
   | ``SchurDelta``          | | ``(0.1)``            | | Selection criteria for Krylov-Schur |
   |                         | | ``<real>``           |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``eigenTol``            | | ``(1e-6)``           | | Eigenvalue tolerance                |
   |                         | | ``<int>``            |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``timeStepper``         | | ``BDF1``             | | Time integration order              |
   |                         | | ``(BDF2)``           |                                       |
   |                         | | ``BDF3``             |                                       |
   +-------------------------+------------------------+---------------------------------------+

.. _tab:stabparams:
