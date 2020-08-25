# KiCad CI/CD test using Spora

This project is a demo of [CI/CD](https://en.wikipedia.org/wiki/Continuous_integration) for [KiCad](https://www.kicad-pcb.org/)

## Objetive

Automate the following tasks:
* ERC and DRC checks
* PDF versions of the schematic and PCB for documentation
* Generation of fabrication files (BoMs, gerbers, drill, position, etc.)

## Tools used

To automate the process here we use:
* [Kiplot](https://github.com/INTI-CMNB/kiplot) to generate gerbers, drill and position files
* [kicad-automation-scripts](https://github.com/INTI-CMNB/kicad-automation-scripts) to run DRC/ERC, prints schematics and PCB
* [KiBoM](https://github.com/INTI-CMNB/KiBoM) to generate HTML and CSV BoMs
* [InteractiveHtmlBom](https://github.com/INTI-CMNB/InteractiveHtmlBom) to generate interactive HTML BoMs
* Docker to integrate KiCad and all the tools in a single package suitable for CI/CD pipelines
* GitLab CI/CD pipeline mechanism

The docker image can be found [here](https://github.com/INTI-CMNB/kicad_auto)

## Test project

As a testbed we are using the [Spora](https://github.com/INTI-CMNB/spora) project. It contains three separated boards:
* **pcb_io** is the I/O module. 2 layers
* **pcb_main** is the main module. 6 layers.
* **pcb_prog** is the programmer interface. 2 layers.

## What we test

The pipeline we test here runs 6 jobs. Two jobs for each PCB. One to test the schematic and generate the associated files and another to test the PCB and generate the associated files.

When a commit affects the any of the schematics, PCBs or the associated Makefiles the pipeline is started. The pipeline succeeds only when the 6 jobs finishes successfully.

An aditional stage collects all the generated stuff in one *artifact*.

When the repo is tagged using a tag with the format **vSEMANTIC_VERSION** the pipeline is started and an additional stage creates a release with the generated files. The associated entries in the *CHANGELOG.md* are used as the release text.

The configuration for this pipeline can be found here: [.gitlab-ci.yml](https://gitlab.com/set-soft/kicad-ci-test-spora/-/blob/master/.gitlab-ci.yml)

An example of automatically generated release can be found here [v1.0.0](https://gitlab.com/set-soft/kicad-ci-test-spora/-/releases/v1.0.0)
[![pipeline status](https://gitlab.com/set-soft/kicad-ci-test-spora/badges/v1.0.0/pipeline.svg)](https://gitlab.com/set-soft/kicad-ci-test-spora/-/commits/v1.0.0)

## Original Spora README

BUILD AWESOME WEARABLES

Open hardware platform for wearables.

Lots of sensors ready to use, program and expand at ease. All packed in an incredible small size.
More info at [Spora web page](https://sporaio.com/).

Final release in [Spora repo](https://github.com/sporaio)

<img src="pcb_main/photos/spora1.jpg" style="width:70%" align="right">


