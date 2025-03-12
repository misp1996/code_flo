<img src="flo-rida-banner.png" alt="Flo Rida" width="800"/>


[![tests](https://github.com/northvolt/flo-rida/actions/workflows/tests.yml/badge.svg)](https://github.com/northvolt/flo-rida/actions/workflows/tests.yml)
[![Documentation: Read the code docs](https://img.shields.io/badge/docs-passing-success)](https://shiny-chainsaw-08d8e12a.pages.github.io/)
[![Package manager: poetry](https://img.shields.io/badge/package%20manager-poetry-purple)](https://python-poetry.org/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

# Flo Rida

Flo Rida *(Flow Writer)* is a lightweight python package for writing flows (tests procedures to be run on batteries) within python. Before Flo Rida, one would need to manually enter flow instructions using the PNE CTS Editor, with no programmatic option available. This resulted in large amounts of repetitive work and was the source of many errors. Flo Rida solves these issues by exposing the flow instructions within python and allowing for templates for common flows utilized so that the process of writing a flow is reduced to passing a small number of conditions. As a result, large lists of conditions can be passed to Flo Rida to automatically generate many flows instantly, without the possibility of human error.

As a conservative estimate, Flo Rida saves the simulation team several days worth of working hours per customer project. We hope Flo Rida can save you time and frustration too.

## :computer: Using Flo Rida
To generate a single flow that follows a common template (e.g. a GITT test), Flo Rida is used in the following manner:
```python
import florida

# Load flow template
gitt_template = florida.templates.GittTemplate()

# Set conditions
cell = florida.Cell(project="PPE High", sample="B1", capacity_ah=160)
gitt_conditions = florida.templates.GittConditions(temperature_degc=25)
flow = gitt_template.generate(cell, gitt_conditions=gitt_conditions)

# Print the flow
print(flow)

# Plot the flow
cycler = florida.VirtualCycler(flow)
cycler.plot()

# Write the flow to file
pne_writer = florida.PneWriter()
pne_writer.write(flow, "flow.sch")
```
However, Flo Rida also offers the user the ability to create flows line-by-line and create templates for common flows. Additionally, Flo Rida includes an in-built helper class QuickFlow to iterate over conditions and generate many flows at once.

Further details can be found in our [examples](https://github.com/northvolt/flo-rida/tree/main/examples) and [documentation](https://shiny-chainsaw-08d8e12a.pages.github.io/).

## :rocket: Installing Flo Rida
### User Install
Flo Rida is available on Linux, MacOS, and Windows. We recommend installing Flo Rida within a [virtual environment](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/) or a [conda environment](https://docs.conda.io/en/latest/). To install Flo Rida, download the `.whl` file for the latest [release](https://github.com/northvolt/flo-rida/releases) and then call
```
pip install path\to\whl\file\florida-<version-number>-py3-non-any.whl
```

### Developer Install
We manage the development of Flo Rida using [poetry](https://python-poetry.org/docs/) and [git](https://git-scm.com/) so you should first follow their relevant installation instructions.

First, create a clone of the Flo Rida repository in your desired location:
```
cd /path/to/your/folder/of/preference
git clone https://github.com/northvolt/flo-rida.git
```
Then enter the Flo Rida directory and install the package and all required dependencies using poetry:
```
cd flo-rida
poetry install
```
*Note: Whilst it is possible to generate a requirements.txt and setup.py using poetry, we currently do not do this to minimize maintenance.*

## Terms of Usage
Whilst we have made a strong effort to prevent errors during the conversion of a flow to binary format (e.g. unit testing of each function) and we are yet to encounter any, we cannot provide one hundred percent confidence in this process. Therefore, by downloading and using Flo Rida, the user accepts full responsibility for checking and ensuring that any generated flows are suitable for running on cycler hardware.

*In future versions of Flo Rida, such concerns will be addressed by allowing the writing of flows to a human readable `.json` format instead of the binary `.sch` format.*

## :email: Get in Touch
If you have any recommended features or find any bugs, please feel free to submit an [issue](https://github.com/northvolt/flo-rida/issues/new) or reach out to us on teams or by email:
- scott.marquis@northvolt.com
- sivakumar.mallikarjunan@northvolt.com
