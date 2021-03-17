nekStab
=======

|Build Status| Global stability framework for Nek5000

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

Main features
~~~~~~~~~~~~~

OUR STABILITY FRAMEWORK
-----------------------

uparam(1) = 0 - > Direct numerical simulation

uparam(1) = 3.- > Direct mode computation

uparam(1) = 3.2 - > Adjoint mode computation

uparam(1) = 3.3 - > Direct-adjoint mode computation for transient growth
analysis
