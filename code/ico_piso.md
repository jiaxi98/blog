#

## IcoFOAM


## PisoFOAM
If one compares the `createFields.H` file of the icoFOAM and picoFOAM, one can find the following additional code showing up in pisoFOAM
```cpp
singlePhaseTransportModel laminarTransport(U, phi);

autoPtr<incompressible::turbulenceModel> turbulence
(
    incompressible::turbulenceModel::New(U, phi, laminarTransport)
);

#include "createMRF.H"
#include "createFvOptions.H"
```
Among which the one of special to us the pointer to a turbulenceModel.


Moreover, in the UEqn of the `pisoFOAM` solver there is one term relates to the turbulence, i.g.
```cpp
fvVectorMatrix UEqn
(
    fvm::ddt(U) + fvm::div(phi, U)
  + MRF.DDt(U)
  + turbulence->divDevReff(U)
 ==
    fvOptions(U)
);
```
which replaces `fvm::laplacian(nu, U)` in UEqn of `icoFOAM`. In `pisoFOAM.C` file there are three another call to the turbulence pointer, i.e.
```cpp
turbulence->validate();
turbulence->correct();
```

## turbulentTransportModel
under the directory: src/TurbulenceModels/incompressible/

```cpp
namespace Foam
{
    namespace incompressible
    {
        typedef IncompressibleTurbulenceModel<transportModel> turbulenceModel;

        typedef laminarModel<turbulenceModel> laminarModel;
        typedef RASModel<turbulenceModel> RASModel;
        typedef LESModel<turbulenceModel> LESModel;
    }
}
```

Recall in the `LESModel.H` file the LESModel is a template class and the template BasicTurbulenceModel is fixed to be turbulenceModel, i.e. IncompressibleTurbulenceModel<transportModel>.


For the discussion on how the `pisoFOAM` call the turbulence model, one can also read this forum[^1].

[^1]: https://www.cfd-online.com/Forums/openfoam/109441-how-turbulence-model-called-openfoam.html
