# Anatomy of OpenFOAM LESModel class

This is the first 


## Smagorinsky

```cpp
template<class BasicTurbulenceModel>
class Smagorinsky
:
    public LESeddyViscosity<BasicTurbulenceModel>
```

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
The LESeddyViscosity class is derived from the eddyViscosity class.
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

## BasicTurbulenceModel