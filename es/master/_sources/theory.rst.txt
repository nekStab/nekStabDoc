==============
Theory
==============

.. _intro_comput_approach:

----------------------
Computational Approach
----------------------

The spatial discretization is based on the spectral element method (SEM) [Patera1984]_, which is a
high-order weighted residual technique similar to the finite element method.   In the SEM, the
solution and data are represented in terms of :math:`N` th-order tensor-product polynomials within each
of :math:`E` deformable hexahedral (brick) elements. Typical discretizations involve
:math:`E`\=100--10,000 elements of order :math:`N`\=8--16 (corresponding to 512--4096 points per
element).  Vectorization and cache efficiency derive from the local lexicographical ordering within
each macro-element and from the fact that the action of discrete operators, which nominally have
:math:`O(EN^6)` nonzeros, can be evaluated in only :math:`O(EN^4)` work and :math:`O(EN^3)` storage
through the use of tensor-product-sum factorization [Orszag1980]_.   The SEM exhibits very little
numerical dispersion and dissipation, which can be important, for example, in stability
calculations, for long time integrations, and for high Reynolds number flows. We refer to
[Denville2002]_ for more details.

Nek5000 solves the unsteady incompressible two-dimensional, axisymmetric, or three-dimensional
Stokes or Navier-Stokes equations with forced or natural convection heat transfer in both
stationary (fixed) or time-dependent geometry. It also solves the compressible Navier-Stokes in the
Low Mach regime, the magnetohydrodynamic equation (MHD).  The solution variables are the fluid
velocity :math:`\mathbf u=(u_{x},u_{y},u_{z})`, the pressure :math:`p`, the temperature :math:`T`.
All of the above field variables are functions of space :math:`{\bf x}=(x,y,z)` and time :math:`t`
in domains :math:`\Omega_f` and/or :math:`\Omega_s` defined in :numref:`fig-walls`.
Additionally Nek5000 can handle conjugate heat transfer problems.

.. _fig-walls:

.. figure:: figs/walls.png
    :align: center
    :figclass: align-center
    :alt: domains

    Computational domain showing respective fluid and solid subdomains, :math:`\Omega_f` and
    :math:`\Omega_s`.  The shared boundaries are denoted :math:`\partial\Omega_f=\partial\Omega_s`
    and the solid boundary which is not shared by fluid is :math:`\overline{\partial\Omega_s}`,
    while the fluid boundary not shared by solid :math:`\overline{\partial\Omega_f}`.

.. _intro_ns:

--------------------------------------
Incompressible Navier-Stokes Equations
--------------------------------------

The governing equations of flow motion in dimensional form are

.. math::
    :label: ns_momentum

    \rho\left(\frac{\partial\mathbf u}{\partial t} +\mathbf u \cdot \nabla \mathbf u\right) = - \nabla p + \nabla \cdot \boldsymbol\tau + \rho {\bf f} \,\, , \text{in } \Omega_f , \quad \text{  (Momentum)  } 

where :math:`\boldsymbol\tau=\mu[\nabla \mathbf u+\nabla \mathbf u^{T}]` and :math:`\mathbf f` is a user defined acceleration.

.. math::
    :label: ns_cont

    \nabla \cdot \mathbf u =0 \,\, , \text{in } \Omega_f, \quad \text{  (Continuity)  }   

If the fluid viscosity is constant in the entire domain the viscous stress tensor can be contracted
:math:`\nabla\cdot\boldsymbol\tau=\mu\Delta \mathbf u`, therefore one may solve the Navier--Stokes equations
in either the stress formulation, or no stress

- Variable viscosity requires the full stress tensor :math:`\nabla \cdot \boldsymbol\tau=\nabla \cdot
  \mu[\nabla \mathbf u+\nabla \mathbf u^{T}]`, and we shall refer to this as the stress formulation
- Constant viscosity leads to a simpler stress tensor :math:`\nabla \cdot \boldsymbol\tau=\mu\Delta \mathbf u`,
  which we refer to as the 'no stress' formulation

.. _intro_ns_nondim:

-----------------------------
Non-Dimensional Navier-Stokes
-----------------------------

Let us introduce the following non-dimensional variables :math:`\mathbf x^*\ = \frac{\mathbf x}{L}`,
:math:`\mathbf u^*\ = \frac{u}{U}`, :math:`t^*\ = \frac{tU}{L}`, and :math:`\mathbf f^* =\frac{\mathbf f L}{U^2}`.  For the pressure scale we have
two options:

- Convective effects are dominant i.e. high velocity flows :math:`p^* = \frac{p}{\rho U^2}`
- Viscous effects are dominant i.e. creeping flows (Stokes flow) :math:`p^* = \frac{p L}{\mu U}`

For highly convective flows we choose the first scaling of the pressure and obtain the
non-dimensional Navier-Stokes:

.. math::
    :label: NS_nondim

    \frac{\partial \mathbf{u^*}}{\partial t^*} + \mathbf{u^*} \cdot \nabla \mathbf{u^*}\ = -\nabla p^* + \frac{1}{Re} \nabla\cdot \boldsymbol\tau^* + \mathbf f^*.

where :math:`\boldsymbol\tau^*=[\nabla \mathbf u^*+\nabla \mathbf u^{*T}]` and :math:`\mathbf f^*` is the dimensionless user defined forcing function, e.g. gravity.

The non-dimensional number here is the Reynolds number :math:`Re=\frac{\rho U L}{\mu}`.

------------------------------------------------
Non-Dimensional Energy / Passive Scalar Equation
------------------------------------------------

A similar non-dimensionalization as for the flow equations using the non-dimensional variables
:math:`\mathbf x^*\ = \frac{\mathbf x}{L}`,  :math:`\mathbf u^*\ = \frac{u}{U}`, :math:`t^*\ =
\frac{t}{L/U}`, :math:`T=\frac{T^*-T_0}{\delta T}` leads to

.. math::
    :label: energy_nondim

    \frac{\partial T^*}{\partial t^*} + \mathbf u^* \cdot \nabla T^* =
      \frac{1}{Pe} \nabla \cdot \nabla T^* + q_{vol}\,\, ,\text{in } \Omega_f\cup \Omega_s  \text{  (Energy)  } 

where :math:`Pe=LU/\alpha`, with :math:`\alpha=k/\rho c_p`.

.. _intro_pass_scal:

---------------
Passive Scalars
---------------

We can additionally solve a convection-diffusion equation for each passive scalar :math:`\phi_i`,
:math:`i = 1,2,\ldots` in :math:`\Omega_f \cup \Omega_s`

.. math::
    :label: pass_scal

    (\rho c_{p})_i \left( \frac{\partial \phi_{i}}{\partial t} + \mathbf u \cdot \nabla \phi_{i} \right) =
    \nabla \cdot (k_i \nabla \phi_{i}) + (q_{vol})_i.

The terminology and restrictions of the temperature equations are retained for the passive scalars,
so that it is the responsibility of the user to convert the notation of the passive scalar
parameters to their thermal analogues.  For example, in the context of mass transfer, the user
should recognize that the values specified for temperature and heat flux will represent
concentration and mass flux, respectively.  Any combination of these equation characteristics is
permissible with the following restrictions. First, the equation must be set to unsteady if it is
time-dependent or if there is any type of advection. For these cases, the steady-state (if it
exists) is found as stable evolution of the initial-value-problem. Secondly, the stress formulation
must be selected if the geometry is time-dependent. In addition, stress formulation must be
employed if there are traction boundary conditions applied on any fluid boundary, or if any mixed
velocity/traction boundaries, such as symmetry and outflow/n, are not aligned with either one of
the Cartesian :math:`x,y` or :math:`z` axes.  Other capabilities of Nek5000 are the linearized
Navier-Stokes for flow stability, magnetohydrodynamic flows etc.

.. _intro_ns_stokes:

.. _intro_linear_eq:

--------------------
Linearized Equations
--------------------

In addition to the basic evolution equations described above, Nek5000 provides support for the
evolution of small perturbations about a base state by solving the *linearized equations*

.. math::
    :label: pertu

    \rho\left(\frac{\partial \mathbf u_i'}{\partial t} + \mathbf u \cdot \nabla {\mathbf u_i}^{'} + \mathbf u_i' \cdot \nabla \mathbf u \right) &=
    - \nabla p_i' + \mu \nabla^2 \mathbf u_i'\\
    \nabla \cdot \mathbf u_i' &= 0 \nonumber

for multiple perturbation fields :math:`i=1,2,\dots` subject to different initial
conditions and (typically) homogeneous boundary conditions.  

These solutions can be evolved concurrently with the base fields :math:`(\mathbf u,p,T)`.  There is
also support for computing perturbation solutions to the Boussinesq equations for natural
convection.  Calculations such as these can be used to estimate Lyapunov exponents of chaotic
flows, etc.

