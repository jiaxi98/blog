# Anatomy of OpenFOAM LESModel class

This is the first blog on understanding the OpenFOAM programming. Our goal is to understand the code structure of the turbulence model for large eddy simulation (LES). We will understand the inheritance relationship between different LES turbulence model classes as well as the 


## Smagorinsky
This class is defined under the directory: src/TurbulenceModels/turbulenceModels/LES/Smagorinsky.
```cpp
template<class BasicTurbulenceModel>
class Smagorinsky
:
    public LESeddyViscosity<BasicTurbulenceModel>
```
It is derived from the template class `LESeddyViscosity<BasicTurbulenceModel>`, same as the WALE model.

Moreover, one can check that one of the constants, e.g. $C_k$ used in the Smagorinsky model is defined in the `Smagorinsky` class while the other constant $C_e$ is defined in `LESModel` class.

For discussion relates to the treatment of the Smagorinsky constant in OpenFOAM, please check (OpenFOAM Smagorinsky)[https://caefn.com/openfoam/smagorinsky-sgs-model]

```cpp
template<class BasicTurbulenceModel>
void SmagorinskyNN<BasicTurbulenceModel>::correct()
{
    if (!this->turbulence_)
    {
        return;
    }

    LESeddyViscosity<BasicTurbulenceModel>::correct();
    correctNut();
}
```
Moreover, the `correct` function of Smagorinsky class first call the `correct` function of LESeddyViscosity class.

## LESeddyViscosity
This class is defined under the directory: src/TurbulenceModels/turbulenceModels/LES/LESeddyViscosity. It is derived from the eddyViscosity class.
```cpp
template<class BasicTurbulenceModel>
class LESeddyViscosity
:
    public eddyViscosity<LESModel<BasicTurbulenceModel>>
```

The constructor function of the LESeddyViscosity class is inherited from the constructor function of eddyViscosity class.
```cpp
template<class BasicTurbulenceModel>
LESeddyViscosity<BasicTurbulenceModel>::LESeddyViscosity
(
    const word& type,
    const alphaField& alpha,
    const rhoField& rho,
    const volVectorField& U,
    const surfaceScalarField& alphaRhoPhi,
    const surfaceScalarField& phi,
    const transportModel& transport,
    const word& propertiesName
)
:
    eddyViscosity<LESModel<BasicTurbulenceModel>>
    (
        type,
        alpha,
        rho,
        U,
        alphaRhoPhi,
        phi,
        transport,
        propertiesName
    )
```


## LESModel
```cpp
template<class BasicTurbulenceModel>
class LESModel
:
    public BasicTurbulenceModel
```

## TurbulenceModel
This class is defined under the directory: src/TurbulenceModels/turbulenceModels.
```cpp
template
<
    class Alpha,
    class Rho,
    class BasicTurbulenceModel,
    class TransportModel
>
class TurbulenceModel
:
    public BasicTurbulenceModel
```
This turbulent class has the similar structure as the `LESModel`, e.g. both derived from `BasicTurbulenceModel`.

## turbulenceModel
This class is defined under the directory: src/TurbulenceModels/turbulenceModels.
```cpp
class turbulenceModel
:
    public IOdictionary
{

protected:

    // Protected data

        const Time& runTime_;
        const fvMesh& mesh_;

        const volVectorField& U_;
        const surfaceScalarField& alphaRhoPhi_;
        const surfaceScalarField& phi_;

        //- Near wall distance boundary field
        nearWallDist y_;


private:

    // Private Member Functions

        //- No copy construct
        turbulenceModel(const turbulenceModel&) = delete;

        //- No copy assignment
        void operator=(const turbulenceModel&) = delete;
}
```

The last important file for understanding the turbulence modeling module in OpenFOAM is `turbulentTransportModel.H` under the directory: src/TurbulenceModels/incompressible/turbulentTransportModels. This file can only be identified if one go through the case file for the `pisoFOAM` solver. For remaining information, please go through the (blog)[url] on `pisoFOAM` solver.


## Remaining confusion
I notice that under OpenFOAM-v2312/src/TurbulenceModels/turbulenceModels directory there are two classes with very similar name but different declaration: `TurbulenceModel`, `turbulenceModel`.
What is the difference of these two classes and their usages?