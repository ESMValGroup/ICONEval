[![LICENSE](https://img.shields.io/badge/License-Apache%202.0-blue)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![DOI:10.5281/zenodo.18937450](https://zenodo.org/badge/DOI/10.5281/zenodo.18937450.svg)](https://doi.org/10.5281/zenodo.18937450)
[![SPEC 0 — Minimum Supported Dependencies](https://img.shields.io/badge/SPEC-0-green?labelColor=%23004811&color=%235CA038)](https://scientific-python.org/specs/spec-0000/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/ESMValGroup/ICONEval/main.svg)](https://results.pre-commit.ci/latest/github/ESMValGroup/ICONEval/main)
[![Run tests](https://github.com/ESMValGroup/ICONEval/actions/workflows/run_tests.yml/badge.svg)](https://github.com/ESMValGroup/ICONEval/actions/workflows/run_tests.yml)
<!-- markdownlint-capture -->
<!-- markdownlint-disable MD049 MD050 -->
<!-- Pytest Coverage Comment:Begin -->
<!-- Pytest Coverage Comment:End -->
<!-- markdownlint-restore -->

---

# ICONEval

ICONEval is a command line tool that facilitates the evaluation of [ICON
model](https://www.icon-model.org/) output with [ESMValTool](doc/esmvaltool.md)
by automatically running a set of predefined ESMValTool recipes. For this,
ICONEval reads a set of template files (ESMValTool recipes and ESMValTool
configuration) and fills these with the information from the ICON simulation(s)
that shall be evaluated.

## Table of Contents

1. [Quick Start](#quick-start)
1. [Prerequisites](#prerequisites)
1. [Installation](#installation)
1. [Customization](#customization)
1. [Common ICON Output Format](#common-icon-output-format)
1. [FAQs](#faqs)

## Quick Start

On Levante, load the module via:

```bash
module use -a /shared/bd1179/modulefiles
module load iconeval
```

The only necessary argument of ICONEval is a valid ICON model output path:

```bash
iconeval path/to/ICON_output
```

This path should point to the directory whose name is identical to the
experiment name of the ICON simulation you want to evaluate, e.g.,
`/root/to/my_amip_run` for the experiment `my_amip_run`. In this case, the
simulation output files should be named `my_amip_run_*_<date>.nc`.

Multiple simulations can be evaluated simultaneously by specifying multiple
ICON output paths.

ICONEval is highly customizable. An example of more realistic command line call
could look like this:

```bash
iconeval path/to/ICON_output path/to/other/ICON_output --tags='["atmosphere", "!subdaily"]' --publish_html=True --timerange=20070101/20080101 --frequency=day
```

Options used here:

- `--tags`: Instead of running the default set of recipes, this will only run
  recipe templates marked with certain [tags](doc/customization.md#tags).
- `--publish_html`: A summary HTML of the evaluation run will be published on a
  **public** website (see also [additional command line
  options](doc/customization.md#additional-command-line-options)).
- `--timerange`: The desired time period that shall be evaluated (see also
  [additional command line
  options](doc/customization.md#additional-command-line-options)).
- `--frequency`: The temporal frequency of the ICON data (see also [additional
  command line options](doc/customization.md#additional-command-line-options)).

For more information on this and a list of all options, run:

```bash
iconeval -- --help
```

or have a look at the section on [Customization](doc/customization.md).

Installing ICONEval also provides the command line tool `publish_html`, which
can be used to publish a summary HTML on a public website for arbitrary
ESMValTool output. For more information, run:

```bash
publish_html -- --help
```

## Example Results

- [Fully coupled historical ICON-XPP
  simulation](https://swift.dkrz.de/v1/dkrz_4eefb34f-8803-415a-bd70-9c455db9a403/iconeval/iconeval_example/index.html)

## Prerequisites

ICONEval needs to run on a machine where the [Slurm Workload
Manager](https://slurm.schedmd.com/) is available for the submission of jobs.

## Installation

On DKRZ's Levante, a pre-installed version of ICONEval is available via a
module. Thus, there is no need to install it yourself as a user on this
machine.

However, on other machines, or if you would like to develop new features for
ICONEval on Levante, an installation from source (*development installation*)
is necessary.

### Levante

To load the ICONEval module on Levante, use:

```bash
module use -a /shared/bd1179/modulefiles
module load iconeval
```

Add these lines to your shell configuration file if you use ICONEval regularly.
[This file](doc/setup_module.md) describes how the ICONEval module is set up.

### Installation from Source (Development Installation)

Installation from source is described [here](doc/install_from_source.md).

## Customization

ICONEval is highly customizable. Detailed information on this can be found
[here](doc/customization.md).

## Common ICON Output Format

To ensure that ICONEval works smoothly, the ICON simulation output should
follow [these criteria](doc/icon_output_format.md) as closely as possible.

## FAQs

A set of frequently asked questions can be found [here](doc/faqs.md).
