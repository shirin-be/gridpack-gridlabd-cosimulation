# gridpack-gridlabd-cosimulation
GridPACK–GridLAB-D co-simulation testbed with HELICS-based coordination and optimization-enabled control.
# GridPACK–GridLAB-D Transportation–Grid Co-Simulation Testbed

This repository contains a transmission–distribution co-simulation testbed integrating **GridPACK**, **GridLAB-D**, and **HELICS**. The framework coordinates a GridPACK transmission-system federate, nine GridLAB-D distribution feeder federates, and a Python-based controller federate.

The controller incorporates the optimization workflow and coordinates the exchange of operational data and control commands during the co-simulation.

## Co-Simulation Configuration

The HELICS federation is configured using:

```text
gpk-gld-cosim.json
```

## Federates

The testbed includes the following HELICS federates:

| Federate name      | Type                               | Execution command                   |
| ------------------ | ---------------------------------- | ----------------------------------- |
| `IEEE123bus_fed`   | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder.glm`   |
| `IEEE123bus_fed_2` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_2.glm` |
| `IEEE123bus_fed_3` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_3.glm` |
| `IEEE123bus_fed_4` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_4.glm` |
| `IEEE123bus_fed_5` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_5.glm` |
| `IEEE123bus_fed_6` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_6.glm` |
| `IEEE123bus_fed_7` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_7.glm` |
| `IEEE123bus_fed_8` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_8.glm` |
| `IEEE123bus_fed_9` | GridLAB-D                          | `gridlabd 1c_IEEE_123_feeder_9.glm` |
| `1c_Controller`    | Python controller and optimization | `python3 controller_fed.py -c 1c`   |
| `gridpack`         | GridPACK transmission federate     | `./build/gpk-left-fed.x`            |



The optimization is integrated into the controller workflow. During the co-simulation, the controller receives system information, executes the optimization process, and communicates the resulting control decisions to the corresponding federates.


The compiled GridPACK federate is generated in:

```text
build/gpk-left-fed.x
```

## Requirements

The following software and libraries are required:

* HELICS
* GridPACK
* GridLAB-D
* Python 3
* CMake
* C++ compiler
* Pyomo
* GLPK or CBC optimization solver


## Building the GridPACK Federate

From the repository root, build the GridPACK federate using:

```bash
rm -rf build
mkdir build
cd build
cmake ..
make
cd ..
```

After successful compilation, confirm that the following executable exists:

```text
build/gpk-left-fed.x
```

## Running the Co-Simulation

From the repository root, launch the complete HELICS federation using:

```bash
helics run --path=gpk-gld-cosim.json
```

This command launches the GridPACK federate, the nine GridLAB-D feeder federates, and the controller federate according to the definitions in `gpk-gld-cosim.json`.
