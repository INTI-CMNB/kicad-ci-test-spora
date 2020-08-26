# KiCad CI/CD test using Spora

![KiCad CI/CD for Spora main board](https://github.com/INTI-CMNB/kicad-ci-test-spora/workflows/KiCad%20CI/CD%20for%20Spora%20main%20board/badge.svg)
![KiCad CI/CD for Spora I/O](https://github.com/INTI-CMNB/kicad-ci-test-spora/workflows/KiCad%20CI/CD%20for%20Spora%20I/O/badge.svg)
![KiCad CI/CD for Spora programmer](https://github.com/INTI-CMNB/kicad-ci-test-spora/workflows/KiCad%20CI/CD%20for%20Spora%20programmer/badge.svg)

This project is a demo of [CI/CD](https://en.wikipedia.org/wiki/Continuous_integration) for [KiCad](https://www.kicad-pcb.org/)

## Objetive

Automate the following tasks:
* ERC and DRC checks
* PDF versions of the schematic and PCB for documentation
* Generation of fabrication files (BoMs, gerbers, drill, position, etc.)

## Tools used

To automate the process here we use:
* [KiBot](https://github.com/INTI-CMNB/KiBot) to generate gerbers, drill, position files and BoMs (HTML, XLSX and CSV)
* [kicad-automation-scripts](https://github.com/INTI-CMNB/kicad-automation-scripts) to run DRC/ERC, prints schematics and PCB
* [InteractiveHtmlBom](https://github.com/INTI-CMNB/InteractiveHtmlBom) to generate interactive HTML BoMs
* [PcbDraw](https://github.com/INTI-CMNB/PcbDraw) to generate the PCB previews using different colors
* Docker to integrate KiCad and all the tools in a single package suitable for CI/CD pipelines
* GitHub CI/CD pipeline mechanism

The docker image can be found [here](https://github.com/INTI-CMNB/kicad_auto)

## Test project

As a testbed we are using the [Spora](https://github.com/INTI-CMNB/spora) project. It contains three separated boards:
* **pcb_io** is the I/O module. 2 layers
* **pcb_main** is the main module. 6 layers.
* **pcb_prog** is the programmer interface. 2 layers.

## What we test

The pipeline we test here runs 3 workflows, one for each PCB. Each workflow runs 4 jobs:

- ERC: Runs the Electrical Rules Check (schematic test).
- Schematic fabrication files: Generates all the outputs related to the schematic. Runs only if the ERC was successful.
- DRC: Runs the Design Rules Check (PCB test).
- PCB fabrication files: Generates all the outputs related to the PCB. Runs only if the DRC was successful.

When a commit affects any of the schematics, PCBs or the associated Makefiles the workflow is started.

The configuration for the workflows can be found here: [.github/workflows/](https://github.com/INTI-CMNB/kicad-ci-test-spora/tree/master/.github/workflows)

## Original Spora README

BUILD AWESOME WEARABLES

Open hardware platform for wearables.

Lots of sensors ready to use, program and expand at ease. All packed in an incredible small size.
More info at [Spora web page](https://sporaio.com/).

Final release in [Spora repo](https://github.com/sporaio)

<img src="pcb_main/photos/spora1.jpg" style="width:70%" align="right">


