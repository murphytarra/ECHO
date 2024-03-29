# Documentation

## Introduction

Reflectometry is a measurement technique which enables spin readout of an electron without collapsing its wavefunction, and can be used in a variety of systems. One such system in which reflectometry can be used measurement of the spin of a quantum dot or a series of quantum dots. Previous analysis of this system has been completed for a two level system coupled with a superconducting resonator, whereby the rotating wave approximation (RWA) is used. 

This package is a tool which allows you to simulate the Dispersion Readout for Multilevel Systems, without the use of the RWA. Here the susceptibility of a double quantum dot (DQD) is calculated using  a cicuit QED formalism and sweeps are carried out over a range of different magnetic fields and magnetitudes of detuning and a plot of the spectrum is simulated.

For further information on the simulation and derivation, please read the included Pdf 'Dispersive Readout of Multilevel Systems'

## Features

The code is no where near complete yet! I still have a couple of tweaks to do and will upload on a regular basis. 

- Dispersive readout for 2 level and 3 level systems
- Ability to change parameters such as spin orbit interaction, Temperature for Dispersive Readouts
- Temperature, Frequency and Coherence Sweeps for different applied Magnetic Fields
- Probability Plots as a function of Temperature
- Ability to plot Eigenvectors of given Hamiltonian

If you have any recommendations or graphs you think might benefit you, please don't hesitate to contact me! 

## Upcoming Features
- Dispersive Readout for N level System 
- Automatic Evaluation of Z matrix given initial Hamiltonian

## Overview

Multilevel Systems and their Dispersive Readouts are simulated using an approach developed by Kohler et al. where the reflected coefficient of a system is dependant on the susceptibility of the system. Scans of the reflected coefficient as a function of detuning and magnetic fields are simulated for a system containing a double quantum dot coupled with a photon. 

## Initialization 

To simulate the dispersive readout scan, first import the package

```javascript
from ECHO import ECHO_3x3 as e3
from ECHO import ECHO_2x2 as e2
```

Create your class

```javascript
P =  e3.ECHO_3x3()
```

## Default Parameters

Initial Parameters for the system are set as follows 

| Name      | Symbol   | Value  |
| :------------- | :----------: | -----------: |
|  Gyromatic Ratios | g1, g2   | 2, 2    |
|  Cavity Decays | k1, k2   | 10e-3, 10e-3    |
|  Coupling Constant | gc   | 0.1    |
|  Frequencies of Photon and DQD | w0, w   | 0.0101, 0.01    |
| Singlet Coupling Constant | delta | 1  |
| Coherence Constant | gamma | 0.1 |
| Spin Orbit Interaction Constant | so | 0.01 |
| Temperature| T | 0.1 |

The Hamiltonian and Z matrix are initially set for two singlet and the triplet minus state with spin orbit interaction.

To change the Hamiltonian, Z matrix or any other parameter, one can change these before running the simulation as follows:

```javascript
P.gamma = 1;
P.so = 0.02;
```

## Running the Simulation for a Three Level System 

To run the simulation, one must use the `.run()` attribute

```javascript
P.run()
```
To change the range of values of detuning and magnetic field, one must input in the parameters into the `.run()` attribute

```javascript
P.run(Bmin = -2, Bmax = 4, emin = -3, emax = 5)
```

To change the resolution of your images, simply increase N, the number of points evaluated between each maximum and minumum of the detuning and magnetic field

```javascript
P.run(N = 250)
```
After running the simulation, an output of the reflection coefficient for a variety of different magnetic fields and detuning parameters.

## Running a simulation for a Two Level System 

To set-up the simulation for a two level system, we first initialize our class: 

```javascript
Q = e2.ECHO_2x2()
```
To run the simulation:

```javascript
Q.run()
```

## Plotting Eigenenergies of Singlets and Triplets 

To plot the eigenenergies of the singlets and triplets of your system for a given Magnetic Field, over a range of detuning values, one can run:

```javascript
P.plot_eigen(B = 1)
```

where here the magnetic field was initially set to one. 

One can change the range of detuning values accordingly

```javascript
P.plot_eigen(B = 1, emin = -5, emax = 5)
```

## Printing out parameters

To print out the relevant parameters for the system, one can use:

```javascript
P.print_parameters()
```

## Save Simulation as .png

If one would like to save the figure simulated for the reflection Coefficient, one must include:

```javascript
P.run(save = True)
```

## Sweeps of Different Parameters

For the three level system, one can simulate the following parameter sweeps:
- Temperature (assuming thermal probabilities)
- Coherence
- Cavity Frequency

To run a temperature sweep for a three level system, we can run the following with the initial parameters shown:

```javascript
P.temp_sweep(B= 1, emin = -3, emax = 3, Tmin = 0.01, Tmax = 1, N = 150)
```

To run a coherence sweep for a three level system, we can run the following with the initial parameters shown: 

```javascript
P.coher_sweep(B= 1, emin = -3, emax = 3, gmin = 0.01, gmax = 1, N = 150)
```

To run a cavity frequency sweep, we run the following: 

```javascript
P.freq_sweep(B= 1, emin = -3, emax = 3, wmin = 0.01, wmax = 1, N = 150)
```




