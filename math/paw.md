# Understanding Projector Augmented-wave Method

## Write at the beginning
This note does not mean to be a comprehensive derivation of the PAW method.
We strongly recommend readers to have a step-by-step derivation
following \cite{rostgaard2009projector}.


## Derivation
The transformation operator $\wht T$ between the all electron wavefunction
$\psi$ and the smoothed wavefunction $\widetilde{\psi}$ is defined as

$$
  \widehat T = \mathbbm{1} + \sum_{a, i}(| \phi_i^a \rangle - | \widetilde{\phi_i^a} \rangle)
  \langle \widetilde{p_i^a}|,
$$

where summations $a, i$ are over the atoms and the atomic orbitals respectively.
The $\phi_i^a, \widetilde{p_i^a}$ are the atomic orbitals of the all-electron and
the smoothed wavefunction respectively. The $\widetilde{p_i^a}$ is the projector
operator of the smoothed wavefunction. The following properties of the
transformation operator $\wht T$ should be kept
in mind for further derivation:
\begin{enumerate}
  \item $\phi_i^a(\mathbf{r}) = \widetilde{\phi_i^a}(\mathbf{r}), \| \mathbf{r} - \mfR^a \| < r_c^a$, i.e.
  the atomic wave function $\phi_i^a$ and the smoothed wavefunction $\widetilde{\phi_i^a}$
  are identical beyond the augmentation sphere $\mathbb{S}^a$ of atom $a$.
  Consequently, the
  transformation operator $\wht T$ is an identity outside all the augmentation spheres.
  \item The projectors $\widetilde{p_i^a}$ are chosen to vanish outside the augmentation
  sphere $\mathbb{S}^a$. Moreover, one requires the following operator to be identity
  inside the augmentation sphere $\mathbb{S}^a$, i.e.:

  $$
    \sum_{i}| \widetilde{p_i^a} \rangle \langle \widetilde{p_i^a}|\Big|_{\mathbb{S}^a} = \mathbbm{1}.
  $$

\end{enumerate}
\JX{Add summary of the generation of the transformation operator. The choice of the
XC functional influences the transformation operator through the atomic wave functions
as they are calculated from atomic scenarios with certain XC functional.}

For future convenience, define the following two one center expansions as

$$
  \psi^a = \sum_{i=1}^{N} \phi_i^a \langle \widetilde{p_i^a}| \widetilde{\psi} \rangle, \quad
  \widetilde{\psi}^a = \sum_{i=1}^{N} \widetilde{p_i^a} \langle \widetilde{p_i^a}| \widetilde{\psi} \rangle.
$$

An immediate corollary of the property \cref{eq:proj} is that

$$
  \widetilde{\psi}^a(\mathbf{r}) = \widetilde{\psi}(\mathbf{r}), \quad \mathbf{r} \in \mathbb{S}^a.  
$$

This is a key identity which leads to an efficient decomposition of the expectation
value discussed in the next subsection.
The all-electron wavefunction $\psi$ can be related to the smoothed wavefunction
$\widetilde{\psi}$ as

$$
  \psi = \widetilde{\psi} + \sum_a (\psi^a - \widetilde{\psi}^a).
$$

### Technique 1: Expectation value of the local operator
We derive the formula for the expectation value of an operator $\wht O$
on a wavefunction $\psi$ based on the decomposition \cref{eq:wavefn-decomp} above:

$$
  \begin{aligned}
    \langle \psi | \wht O | \psi \rangle = & \ 
    \langle \widetilde{\psi} + \sum_a (\psi^a - \widetilde{\psi}^a) | \wht O 
    | \widetilde{\psi} + \sum_a (\psi^a - \widetilde{\psi}^a) \rangle    \\
    = & \ \langle \widetilde{\psi} | \wht O | \widetilde{\psi}  \rangle + 
    \sum_a \langle \widetilde{\psi} | \wht O | \sum_a (\psi^a - \widetilde{\psi}^a) \rangle +
    \sum_{a, a'} \langle (\psi^a - \widetilde{\psi}^a) | \wht O | (\psi^{a'} - \widetilde{\psi}^{a'})  \rangle\\
    = & \ \langle \widetilde{\psi} | \wht O | \widetilde{\psi}  \rangle + 
    \sum_a \lp \langle \psi^a | \wht O | \psi^a \rangle - 
    \langle \widetilde{\psi}^a | \wht O | \widetilde{\psi}^a \rangle \rp  \\
    & \  + \sum_{a \neq a'} \langle (\psi^a - \widetilde{\psi}^a) | \wht O 
    | (\psi^{a'} - \widetilde{\psi}^{a'})  \rangle
    + 2\sum_{a} \langle (\widetilde{\psi} - \widetilde{\psi}^a) | \wht O | (\psi^{a} - \widetilde{\psi}^{a})  \rangle
  \end{aligned}
$$

Now, using the fact that $\psi^a, \widetilde{\psi}^a$ only differs inside the augmentation
sphere $\mathbb{S}^a$ and different augmentation spheres are disjoint, we conclude
that the first term in the last line vanishes. The second term also vanishes due to
the fact \cref{eq:aux1}.
This reduces the original expectation to the
expectation value evaluated on the smoothed wavefunction $\widetilde{\psi}$ and the
difference of the expectation value of two one-center expansions inside the
augmentation sphere $\mathbb{S}^a$. This can be further simplified as

$$
  \begin{aligned}
    \langle \psi^a | \wht O | \psi^a \rangle - 
    \langle \widetilde{\psi}^a | \wht O | \widetilde{\psi}^a \rangle
    =  \sum_{ij} \lp \langle \phi_i^a | \wht O | \phi_j^a \rangle - 
    \langle \widetilde{\phi_i^a} | \wht O | \widetilde{\phi_j^a} \rangle \rp 
    \langle \widetilde{\psi} | \widetilde{p_i^a} \rangle \langle \widetilde{p_j^a} | \widetilde{\psi} \rangle,
  \end{aligned}
$$


One immediate consequence of the above decomposition is for the density operator which is
definitely local:

$$
  \begin{aligned}
    n(\mathbf{r}) = & \ \sum_n^{\text{val}} f_n \langle \psi_n | \mathbf{r} \rangle
    \langle \mathbf{r} | \psi_n \rangle
    + \sum_{a,c}^{\text{core}} |\psi^{a, c}(\mathbf{r})|^2  \\
    = & \ \sum_n f_n \lp | \widetilde{\psi}_n (\mathbf{r}) |^2 + 
    \sum_a \lp {\phi_i^{a}}^*(\mathbf{r}) \phi_j^a(\mathbf{r}) - 
    \widetilde{\phi_i^{a}}^*(\mathbf{r}) \widetilde{\phi_j^a}(\mathbf{r}) \rp 
    \langle \widetilde{\psi}_n | \widetilde{p_i^a} \rangle \langle \widetilde{p_j^a} | \widetilde{\psi}_n \rangle \rp 
    + \sum_{a,c}^{\text{core}} |\psi^{a, c}(\mathbf{r})|^2  \\
    = & \ \sum_n f_n | \widetilde{\psi}_n (\mathbf{r}) |^2 + \sum_{a,i,j} \lp {\phi_i^{a}}^*(\mathbf{r}) \phi_j^a(\mathbf{r}) - 
    \widetilde{\phi_i^{a}}^*(\mathbf{r}) \widetilde{\phi_j^a}(\mathbf{r}) \rp D_{ij}^a
    + \sum_{a,c}^{\text{core}} |\psi^{a, c}(\mathbf{r})|^2,
  \end{aligned}
$$

where $D_{ij}^a = \sum_nf_n\langle \widetilde{\psi}_n | \widetilde{p_i^a} \rangle
\langle \widetilde{p_j^a} | \widetilde{\psi}_n \rangle$
these quantities are changing with $\widetilde{\psi}$ and contributing
to the total energy. From the definition one conclude that
the $D_{ij}^a$ is Hermitian w.r.t. $i, j$, i.e. $D_{ij}^a = {D_{ji}^{a}}^*$.
And this term are named the augmentation charge in most pseudoppotential files.
For future convenience, we introduce the following decompoistion
of the charge density, parallel to the decomposition of the wavefunction \cref{eq:wavefn-decomp}

$$
  \begin{aligned}
    n = & \ \widetilde{n} + \sum_a (n^a - \widetilde{n}^a), \\
    \widetilde{n} = & \ \sum_n f_n | \widetilde{\psi}_n (\mathbf{r}) |^2 + \sum_a \widetilde{n}_c^a, \\
    n^a = & \ \sum_{i,j} {\phi_i^{a}}^*(\mathbf{r}) \phi_j^a(\mathbf{r}) D_{ij}^a + n_c^a,   \\
    \widetilde{n}^a = & \ \sum_{i,j} \widetilde{\phi_i^{a}}^*(\mathbf{r}) \widetilde{\phi_j^a}(\mathbf{r}) D_{ij}^a + \widetilde{n}_c^a.   \\
  \end{aligned}
$$

In above decomposition, the $n_c^a$ is the charge density of the core electrons
fixed according to the frozen core approximation. The $\widetilde{n}_c^a$ is the 
smoothed charge density for core electrons which is guaranteed to be identical
to the $n_c^a$ outside the augmentation sphere $\mathbb{S}^a$. Again, parallel to the
result \cref{eq:aux1}, we have

$$
  \widetilde{n}^a(\mathbf{r}) = \widetilde{n}(\mathbf{r}), \quad \mathbf{r} \in \mathbb{S}^a.
$$

This will be a key ingredient to the decomposition of the Coulomb energy in \cref{sec:tech3}.

### Technique 2: Multipole moment expansion construction of the compensation charge
The multipole moment expansion of the Coulomb potential is the key ingredient to
construct a compensation charge leading to a localized effective potential. Recall
that the solution of the Poisson equation by its Green's function is given by

$$
    V(\bm r) = & -\int_{\mbR^3} \frac{\rho(\bm r')}{|\bm r - \bm r'|} d\bm r'.
$$

One can expand the Green's function in the spherical harmonics, a.k.a. the multipole
moment expansion, as

$$
  \begin{aligned}
    \frac{1}{|\bm r - \bm r'|} = \sum_{l=0}\sum_{m=-l}^{l} \frac{4\pi}{2l + 1}
    \frac{r_<^l}{r_>^{l+1}} Y_{lm}^*(\theta', \phi') Y_{lm}(\theta, \phi).
  \end{aligned}
$$

One interpretation of this expansion is that the Coulomb interaction only
exists between the spherical harmonics of the same order $L$.
Now, expanding the density
$\rho(\bm r') = \sum_{l=0}\sum_{m = -l}^l$
$\rho_{lm}(r')Y_{lm}(\theta', \phi')$
in the spherical harmonics and substituting to \cref{eq:green} gives

$$
  \begin{aligned}
    V(\bm r) = & -\sum_{l=0}\sum_{m=-l}^{l} \frac{4\pi}{2l + 1} \int_0^{\infty}
    \frac{r_<^l}{r_>^{l+1}} Y_{lm}(\theta, \phi)\rho_{lm}(r') dr'.
  \end{aligned}
$$

If we assume that the density $\rho(r')$ is supported in the sphere of radius $r_c$, i.e.
$\rho_{lm}(r') = 0, r' > r_c$, then for any $\| \mathbf{r} \| > r_c$, one has $V(\bm r) = 0$.
Therefore, if we can choose $\rho_{lm}(r')$ so that the integral vanishes, i.e.

$$
  \int_{B_{r_c}} r^l Y_{lm}^*(\widehat{\mathbf{r}}) \rho(\mathbf{r}) d\mathbf{r} = 0.
$$

The Coulomb potential generated by this charge density will be zero outside the augmentation
sphere and the Coulomb interaction energy is localized to the integrals over the
augmentation spheres. This is the key idea of the compensation charge which localized
the nonlocal Coulomb interaction energy.


### Technique 3: Expectation value of the nonlocal Coulomb energy
Now, with the following decomposition of the charge system inside the unit cell

$$
  \rho = \widetilde{n} + \sum_a (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a} + \widetilde{Z^a}),
$$

the Coulomb energy can be expressed as 

$$
    E_{\text{Coul}} = & ((\widetilde{n} + \sum_a (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a} + \widetilde{Z^a})))\\
    = & \ ((\widetilde{n} + \sum_a \widetilde{Z^a})) + ((\sum_a (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a}))) \\
    & \ + 2(\widetilde{n} + \sum_a \widetilde{Z^a}|\sum_a (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a}))\\
    = & \ \widetilde{E_{\text{Coul}}} + \sum_a ((n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a})) + 
    2\sum_a(\widetilde{n}^a + \widetilde{Z^a}|n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a})\\
    = & \ \widetilde{E_{\text{Coul}}} + \sum_a ((n^a + Z^a)) - \sum_a((\widetilde{n}^a + \widetilde{Z^a})).
$$

Notice that since $n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a}$ only has non-vanishing potential
inside the augmentation sphere $\mathbb{S}^a$, implying that one does not even bother
to calculate the interaction energy between the different unit cells! \textbf{No Ewald summations
are needed, only simple integrals over the radial coordinate.}


## Full derivation of the total energy in PAW formulation
In this section, we provide the full derivation of the total energy in the
PAW formulation.
### The kinetic energy
The kinetic energy operator is a local operator and its expectation value follows
directly from the results in \cref{sec:local-exp}, i.e.

$$
  \begin{aligned}
    E_{\text{kin}} = & \ \widetilde{E_{\text{kin}}} + E_{\text{kin}}^c +
    \half\sum_{a,i,j}D_{ij}^a
    \int_{\mathbb{S}^a}\lp \nabla{\phi_i^{a}}^*(\mathbf{r}) \nabla\phi_j^a(\mathbf{r}) - 
    \nabla\widetilde{\phi_i^{a}}^*(\mathbf{r}) \nabla\widetilde{\phi_j^a}(\mathbf{r}) \rp d\mathbf{r}.
  \end{aligned}
$$

Notice that the kinetic energy of the core electrons does not depend on the
crystalline structure and can be ignored in the geometry optimization or
molecular dynamics simulation. The last term can be understood as a nonlocal
potential written as

$$
  V_{\text{n-loc}}^{\text{kin}} = \half\sum_{a,i,j}| \widetilde{p_i^a} \rangle \langle \widetilde{p_j^a}|
  \int_{\mathbb{S}^a}\lp \nabla{\phi_i^{a}}^*(\mathbf{r}) \nabla\phi_j^a(\mathbf{r}) - 
  \nabla\widetilde{\phi_i^{a}}^*(\mathbf{r}) \nabla\widetilde{\phi_j^a}(\mathbf{r}) \rp d\mathbf{r}
$$


### The XC energy
For the XC functional of LDA and GGA type, the XC energy is a local operator
and the evaluation is given by

$$
  \begin{aligned}
    E_{\text{XC}} = & \ \wtd E_{\text{XC}} + 
    \sum_{a}(E_{\text{XC}}^a - \wtd E_{\text{XC}}^a),
  \end{aligned}
$$

where both $E_{\text{XC}}^a, \wtd E_{\text{XC}}^a$ can only be integrated over the
augmentation sphere $\mathbb{S}^a$.

### The compensation charge
Recall the multipole moment constraint on the compensation charge is given by

$$
  \int_{B_{r_c}} r^l Y_{L}^*(\widehat{\mathbf{r}}) (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a})
  (\mathbf{r} + \mfR^a) d\mathbf{r} = 0.
$$

Taking $L=0 \rightarrow l=m=0$, one obtains

$$
  \int_{B_{r_c}} (n^a - \widetilde{n}^a + Z^a - \widetilde{Z^a}) (\mathbf{r} + \mfR^a) d\mathbf{r} = 0,
$$

corresponding to the charge neutrality condition inside the augmentation sphere.
Representing the compensation charge in the spherical harmonics as

$$
  \widetilde{Z^a}(\mathbf{r} + \mfR^a) = \sum_{L} Q_{L}^a \widetilde{g_{L}^a}(\widehat{\mathbf{r}}),
$$

where $g_{L}^a(\mathbf{r}) = g_L(r)Y_L(\widehat{\mathbf{r}})$ such that $g_L$ vanishes for
$r>r_c$ and has a unit l-th moment. Therefore, the coefficients $Q_{L}^a$ can be
determined via 

$$
  \int_{B_{r_c}} r^l \widetilde{Z^a}(\mathbf{r})Y_L^*(\widehat{\mathbf{r}}) d\mathbf{r}  
  = \int_{B_{r_c}} r^l g_L^a(\mathbf{r})Y_L^*(\widehat{\mathbf{r}}) d\mathbf{r} 
  = \int_0^{r_c} Q_L^a g_L(r) r^l dr = Q_L^a.
$$

Using the \cref{eq:multipole-moment} and \cref{eq:density-decomp},
one can express the $Q_L^a$ in terms of $D_{ij}^a$ as

$$
    Q_L^a = & \ \int_{B_{r_c}} r^l Y_{L}^*(\widehat{\mathbf{r}}) (n^a - \widetilde{n}^a + Z^a)
    (\mathbf{r} + \mfR^a) d\mathbf{r}   \\
  = & \ \sum_{ij}D_{ij}^a \int_{B_{r_c}} r^l Y_{L}^*(\widehat{\mathbf{r}})
  \lp {\phi_i^{a}}^*(\mathbf{r}) \phi_j^a(\mathbf{r}) - \widetilde{\phi_i^{a}}^*(\mathbf{r}) \widetilde{\phi_j^a}(\mathbf{r}) \rp
  d\mathbf{r} \\
  & \ + \frac{\delta_{L0}}{\sqrt{4\pi}}\lp \int_0^{r_c}4\pi r^2(n_c^a(r) - \widetilde{n}_c^a(r))dr
  - Z^a\rp := \sum_{ij}D_{ij}^a\Delta_{Lij}^a + \delta_{L0}\Delta_{0}^a,  \\
$$

where we has used the fact that both $n_c^a, \widetilde{n}_c^a$ are radial and only
contribute the $l=0$ term and $\delta_{L0}$ is the Kronecker delta symbol.
Intuitively speaking, the larger the augmentation sphere radius $r_c$, the less 
restrictive to the compensation charge $\widetilde{Z^a}$ since the multipole moment
expansion requires the potentail outside the augmentation sphere to be zero.
Consequently, the compensation charge can have better smoothness property.

As illustrated in \cref{eq:coulomb-decomp}, Coulomb interaction between $\widetilde{n}$ and
$\widetilde{Z^a}$ is calculated instead of $n^a - \widetilde{n}^a + Z^a$. In planewave basis, this
calculation is efficient only if the cutoff of $\widetilde{Z^a}$ is much smaller than that of
the $n^a - \widetilde{n}^a + Z^a$. We investigate this seriously in the appendix
\cref{sec:compensation-theory}.

### The nonlocal Coulomb energy
Now, we treat the most complicated Coulomb energy term in the decomposition of the
total energy. Recall the decomposition of $n^a, \widetilde{n}^a$ in \cref{eq:density-decomp}, we have:

$$
  \begin{aligned}
    & \ ((n^a + Z^a)) - ((\widetilde{n}^a + \widetilde{Z^a})) \\
    = & \ ((n^a)) + 2(n^a|Z^a) + ((Z^a)) - ((\widetilde{n}^a)) 
    - 2(\widetilde{n}^a|\widetilde{Z^a}) - ((\widetilde{Z^a})) \\
    = & \ ((n_c^a)) + 2\sum_{ij}D_{ij}^a(n_c^a|{\phi_i^{a}}^* \phi_j^a) + 
    \sum_{ij,i'j'}D_{ij}^aD_{i'j'}^a({\phi_{i'}^{a}}^* \phi_{j'}^a|{\phi_i^{a}}^* \phi_j^a) 
    + 2\sum_{ij}D_{ij}^a(Z^a|{\phi_i^{a}}^* \phi_j^a)  \\
    & \ + 2(n_c^a|Z^a)
    + ((Z^a)) - ((\widetilde{n}_c^a)) - 2\sum_{ij}D_{ij}^a(\widetilde{n}_c^a|\widetilde{\phi_i^{a}}^* \widetilde{\phi_j^a}) -
    \sum_{ij,i'j'}D_{ij}^aD_{i'j'}^a
    (\wtd {\phi_{i'}^{a}}^* \wtd \phi_{j'}^a|\widetilde{\phi_i^{a}}^* \widetilde{\phi_j^a}) \\
    & \ - 2\sum_L Q_L^a(\widetilde{n}_c^a|\widetilde{g_L^a})
    - 2\sum_{ij, L}D_{ij}^aQ_L^a(\widetilde{g_L^a}|\widetilde{\phi_i^{a}}^* \widetilde{\phi_j^a})
    - \sum_{L, L'}Q_L^aQ_{L'}^a(\wtd g_{L'}^a|\widetilde{g_L^a})  \\
    = & \ ((n_c^a)) - ((\widetilde{n}_c^a)) + 2(n_c^a|Z^a) + ((Z^a)) 
    + 2\sum_{ij}D_{ij}^a\lp (Z^a + n_c^a|{\phi_i^{a}}^* \phi_j^a) - 
    (\widetilde{n}_c^a|\widetilde{\phi_i^{a}}^* \widetilde{\phi_j^a}) \rp \\
    & \ + \sum_{ij,i'j'}D_{ij}^aD_{i'j'}^a\lp ({\phi_{i'}^{a}}^* \phi_{j'}^a|{\phi_i^{a}}^* \phi_j^a)
    - (\wtd {\phi_{i'}^{a}}^* \wtd \phi_{j'}^a|\widetilde{\phi_i^{a}}^* \widetilde{\phi_j^a}) \rp \\
    & \ - 2\sum_L Q_L^a(\widetilde{n}_c^a|\widetilde{g_L^a}) -
    2\sum_{ij, L}D_{ij}^aQ_L^a(\widetilde{g_L^a}|\wtd{\phi_i^{a}}^* \widetilde{\phi_j^a})
    - \sum_{L, L'}Q_L^{a}Q_{L'}^a(\wtd g_{L'}^a|\widetilde{g_L^a})  \\
  \end{aligned}
$$

\JX{Special attention should be paid to $\widetilde{Z^a}$ since it is the only non-real
term. Is this correct? Need double check on the Hermitian conjugate.}
One can further expands the above expression by plugging in \cref{eq:aux2}:

$$
    & \ ((n_c^a)) - ((\widetilde{n}_c^a)) + 2(n_c^a|Z^a) + ((Z^a)) 
    - 2\sum_L \Delta_0^a(\widetilde{n}_c^a|\widetilde{g_L^a}) 
    - \sum_{L}\lp\Delta_0^a\rp^2(\widetilde{g_{L}^a}|\widetilde{g_L^a})\\
    & \ + 2\sum_{ij}D_{ij}^a\lp (Z^a + n_c^a|\phi_i^{a*} \phi_j^a) 
    - (\widetilde{n}_c^a|\wtd \phi_i^{a*} \widetilde{\phi_j^a})  \right. \\
    & \ \left. - 2\sum_L\Delta_{Lij}^a(\widetilde{n}_c^a|\widetilde{g_L^a})
    - 2\Delta_0^a(\wtd g_0^a|\wtd{\phi_i^{a}}^* \widetilde{\phi_j^a})
    - 2\Delta_0^a\sum_L\Delta_{Lij}^a (\widetilde{g_{L}^a}|\widetilde{g_L^a})\rp \\
    & \ + \sum_{ij,i'j'}D_{ij}^aD_{i'j'}^a\lp
    (\phi_{i'}^{a*} \phi_{j'}^a|\phi_i^{a*} \phi_j^a)
    - (\wtd \phi_{i'}^{a*} \wtd \phi_{j'}^a|\wtd \phi_i^{a*} \widetilde{\phi_j^a}) \right. \\
    & \ \left. - 2\sum_L\Delta_{Lij}^a(\widetilde{g_L^a}|\phi_i^{a*} \widetilde{\phi_j^a}) 
    - \sum_{L}\Delta_{Lij}^a\Delta_{Li'j'}^a(\widetilde{g_{L}^a}|\widetilde{g_L^a}) \rp,
$$

where the terms appearing above is defined in \cref{eq:aux2}.
Recall in \cref{sec:tech3} we have mentioned that the above integral only needs to be
evaluated over the augmentation sphere $\mathbb{S}^a$ and no interaction between different
unit cells is required. Next, use the multipole moment expansion of the Coulomb kernel
one can transform all the integrals above to a 2D integral as follows:

$$
  \begin{aligned}
    & \ \int_{B_{r_c}\times B_{r_c'}} d\mathbf{r} d\mathbf{r}' f^{*}(\mathbf{r}) g(\mathbf{r}')
    \frac{1}{\norml \mathbf{r} - \mathbf{r}'\normr}   \\
    = & \ \sum_L \frac{4\pi}{2l + 1}
    \int_0^{r_c}dr f_L^*(r)\lp \int_0^{r}dr' \frac{{r'}^l}{r^{l+1}} g_L(r') +
    \int_r^{r_c'}dr' \frac{r^l}{{r'}^{l+1}} g_L(r') \rp,
  \end{aligned}
$$

where $f_L, g_L$ is the spherical harmonics expansion coefficients of $f, g$
respectively.
The remaining terms related to the smoothed density, e.g.
$\widetilde{E_{\text{Coul}}} = ((\widetilde{n} + \sum_a \widetilde{Z^a}))$ can be evaluated by
calculating the Fourier coefficients of the radial-grid based $\widetilde{Z^a}$
and using original plane-wave methods. Moreover, all the energy parts appearing
in the first line of \cref{eq:paw-coulomb} remain to be constant due to the
frozen core approximation, even in molecular dynamics. Therefore, their
implementation can be ignored in the total energy calculation.

## Comparison between the PAW and USPP
As stated in the Sec. II.F of \cite{kresse1999ultrasoft}: \textit{the equations for
ultrasoft pseudopotentials can be obtained readily from the modified PAW total energy
functional by linearization it around the atomic reference occupancies.}

Therefore, a naive understanding to think about the total energy of the USPP
method is to drop all the quadratic terms in the PAW total energy functional
of $D_{ij}^a$, i.e.

$$
  \begin{aligned}
    & \ \sum_{ij,i'j'}D_{ij}^aD_{i'j'}^a\lp
    (\phi_{i'}^{a*} \phi_{j'}^a|\phi_i^{a*} \phi_j^a)
    - (\wtd \phi_{i'}^{a*} \wtd \phi_{j'}^a|\wtd \phi_i^{a*} \widetilde{\phi_j^a}) \right. \\
    & \ \left. - 2\sum_L\Delta_{Lij}^a(\widetilde{g_L^a}|\phi_i^{a*} \widetilde{\phi_j^a}) 
    - \sum_{L}\Delta_{Lij}^a\Delta_{Li'j'}^a(\widetilde{g_{L}^a}|\widetilde{g_L^a}) \rp
  \end{aligned}
$$
