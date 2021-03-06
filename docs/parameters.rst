Parameters 
==========

Current form of input via uparams 
--------------------------------- 

-  uparam(1) = computation mode 

               0: DNS, 
               1:stabilization, 
               3   :  stability with direct,
               3.2:stability with adjoint,
               3.3:stability with transientGrowth
               
-  uparam(2) = restart vector for stability (optional)

-  uparam(3) = stabilzation technique (1:SFD)

-  uparam(4) = target mode estimated Strouhal

-  uparam(5) = target mode estimated growth rate

-  uparam(6) =

-  uparam(7) =

-  uparam(8) = sponge side left length (e.g. 1)

-  uparam(9) = sponge side right length (e.g. 5)

-  uparam(10) = sponge strenght (>0 to activate e.g. 1.7)


Future update via parser 
------------------------ 

-----------------------------------
Stability File (.pars)
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
   | ``baseFlow``            | | ``(steady)``         | | Base flow type                      |
   |                         | | ``mean``             |                                       |
   |                         | | ``periodic``         |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``forcing` `            | | ``(none)``           | | Optional forcing for evolOperator   |
   |                         | | ``prescribed``       |                                       |
   |                         | | ``reynoldsStess``    |                                       |
   |                         | | ``loadFromFile``     |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``baseFlow``            | | ``usric``            | | Base flow source                    |
   |                         | | ``loadFromFile``     |                                       |
   |                         | | ``periodic``         |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``inSeed``              | | ``noise``            | | Initial seed                        |
   |                         | | ``symmetric``        |                                       |
   |                         | | ``loadFromFile``     |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``krylovDimension``     | | ``<int>``            | | Krylov-space dimension              |
   |                         | |                      |   kdim <= kdimmax                     |
   +-------------------------+------------------------+---------------------------------------+
   | ``SchurTarget``         | | ``<int>``            | | Convergence target for Krylov-Schur |
   |                         | |                      | | schur_tgt < kdim                    |
   +-------------------------+------------------------+---------------------------------------+
   | ``SchurDelta``          | | ``(0.1)``            | | Selection criteria for Krylov-Schur |
   |                         | | ``<real>``           | | schur_del > 0                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``eigenTol``            | | ``(1e-6)``           | | Eigenvalue tolerance                |
   |                         | | ``<real>``           | | eigen_tol > 0                       |
   +-------------------------+------------------------+---------------------------------------+
.. _tab:stabparams:


.. _tab:stabparamsbf:
.. table:: ``BASE_FLOW`` keys in the ``.pars`` file

   +-------------------------+------------------------+---------------------------------------+
   | | Key                   | | Value(s)             | | Description                         |
   +=========================+========================+=======================================+
   | ``baseFlowType``        | | ``(steady)``         | | Base flow type                      |
   |                         | | ``periodic``         |                                       |
   |                         | | ``mean``             |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``baseFlowMethod``      | | ``(SFD)``            | | Evolution operator                  |
   |                         | | ``TDF``              |                                       |
   |                         | | ``newtown``          |                                       |
   |                         | | ``boostCOnv``        |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``tolerance``           | | ``(auto)``           | |                                     |
   |                         | | ``<real>``           | |                                     |
   +-------------------------+------------------------+---------------------------------------+

.. _tab:stabparamsbf:

.. _tab:stabparamssfd:
.. table:: ``SFD`` keys in the ``.pars`` file
   +-------------------------+------------------------+---------------------------------------+
   | | Key                   | | Value(s)             | | Description                         |
   +=========================+========================+=======================================+
   | ``temporalOrder``       | | ``(AB3)``            | | Base flow type                      |
   |                         | | ``AB2``              |                                       |
   |                         | | ``Euler``            |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``method``              | | ``(akervic)``        | | Evolution operator                  |
   |                         | | ``casacuberta``      |                                       |
   |                         | | ``prescribed``       |                                       |
   +-------------------------+------------------------+---------------------------------------+
   | ``cutoff``              | | ``<float>``          | |                                     |
   +-------------------------+------------------------+---------------------------------------+
   | ``gain``                | | ``<float>``          | |                                     |
   +-------------------------+------------------------+---------------------------------------+
   | ``tolerance``           | | ``<float>``          | |                                     |
   +-------------------------+------------------------+---------------------------------------+
   | ``scalar``              | | ``(no)``             | |                                     |
   |                         | | `` yes``             | |                                     |
   +-------------------------+------------------------+---------------------------------------+
.. _tab:stabparamssfd:

.. _tab:stabparamstdf:
.. table:: ``TDF`` keys in the ``.pars`` file
   +-------------------------+------------------------+---------------------------------------+
   | | Key                   | | Value(s)             | | Description                         |
   +=========================+========================+=======================================+
   | ``baseFlowType``        | | ``(steady)``         | | Base flow type                      |
   +-------------------------+------------------------+---------------------------------------+
.. _tab:stabparamstdf:

.. _tab:stabparamsbc:
.. table:: ``BOOSTCOV`` keys in the ``.pars`` file
   +-------------------------+------------------------+---------------------------------------+
   | | Key                   | | Value(s)             | | Description                         |
   +=========================+========================+=======================================+
   | ``baseFlowType``        | | ``(steady)``         | | Base flow type                      |
   +-------------------------+------------------------+---------------------------------------+
.. _tab:stabparamsbc: