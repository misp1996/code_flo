# Contributing to Flo Rida

If you'd like to contribute to Flo Rida (thanks!), please have a look at the [guidelines below](#workflow).

If you're already familiar with our workflow, maybe have a quick look at the [pre-commit checks](#pre-commit-checks) directly below.

## Software Scope
At the moment, Flo Rida covers the creation of flows within python and the writing of these
flows to PNE binary format. In general, we would like to keep Flo Rida lightweight and
limit the scope of Flo Rida to the reading, writing, and creation of flows.

We would normally consider the following types of extensions to be within the scope
of Flo Rida:

- output to different cycler formats
- additional human-readable output formats
- support for additional input formats

We are always open to discussions for new features but we would probably
consider the following types of extensions to be out-of-scope:

- a graphical user interface to write flows
- processing data collected from cyclers (check out the excellent [valibrary](https://github.com/northvolt/validation-data-analysis) instead)


## Pre-commit checks

Before you commit any code, please perform the following checks:

- [ ] No style issues: `$ flake8`
- [ ] All tests pass: `$ poetry run python -m unittest`
- [ ] The documentation builds: `cd docs` and then do `.\make.bat html` in Windows or  `make html` in Linux/Mac

## Workflow

We use [GIT](https://en.wikipedia.org/wiki/Git) and [GitHub](https://en.wikipedia.org/wiki/GitHub) to coordinate our work. When making any kind of update, we try to follow the procedure below.

### A. Before you begin

1. Create an [issue](https://guides.github.com/features/issues/) where new proposals can be discussed before any coding is done. You can check out [our software scope](#software-scope) for an idea on things to work on.
2. Create a [branch](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository/) of this repo (ideally on your own [fork](https://help.github.com/articles/fork-a-repo/)), where all changes will be made
3. Download the source code onto your local system, by [cloning](https://help.github.com/articles/cloning-a-repository/) the repository (or your fork of the repository).
4. Install Flo Rida using Poetry.
5. [Test](#testing) if your installation worked, using the test script: `$ poetry run python -m unittest`.

You now have everything you need to start making changes!

### B. Writing your code

6. Make sure to follow our [coding style guidelines](#coding-style-guidelines).
7. Commit your changes to your branch with [useful, descriptive commit messages](https://chris.beams.io/posts/git-commit/): Remember these should still make sense a few months ahead in time. While developing, you can keep using the GitHub issue you're working on as a place for discussion. [Refer to your commits](https://stackoverflow.com/questions/8910271/how-can-i-reference-a-commit-in-an-issue-comment-on-github) when discussing specific lines of code.
8. If you want to add a dependency on another library, or re-use code you found somewhere else, have a look at [these guidelines](#dependencies-and-reusing-code).

### C. Merging your changes with Flo Rida

10. [Test your code!](#testing)
11. Flo Rida has online documentation at https://shiny-chainsaw-08d8e12a.pages.github.io/. To make sure any new methods or classes you added show up there, please read the [documentation](#documentation) section.
12. If you added a major new feature, perhaps it should be showcased in an [example script](#example-scripts).
13. When you feel your code is finished, or at least warrants serious discussion, run the [pre-commit checks](#pre-commit-checks) and then create a [pull request](https://help.github.com/articles/about-pull-requests/) (PR) on [Flo Ridas's GitHub page](https://github.com/northvolt/flo-rida).
14. Once a PR has been created, it will be reviewed by any member of the community. Changes might be suggested which you can make by simply adding new commits to the branch. When everything's finished, someone with the right GitHub permissions will merge your changes into Flo Rida main repository.
15. After merging, please your changes to the [latest draft version](https://github.com/northvolt/flo-rida/releases)

Finally, if you really, really, _really_ love developing Flo Rida, have a look at the current [project infrastructure](#infrastructure).


## Coding style guidelines

Flo Rida follows the [PEP8 recommendations](https://www.python.org/dev/peps/pep-0008/) for coding style. These are very common guidelines, and community tools have been developed to check how well projects implement them.

### Flake8

We use [flake8](http://flake8.pycqa.org/en/latest/) to check our PEP8 adherence. To try this on your system, navigate to the Flo Rida directory in a console and type

```bash
flake8
```
Flake8 is configured inside the file `.flake8`, allowing us to ignore some errors. If you think this should be added or removed, please submit an [issue](#issues)

When you commit your changes they will be checked against flake8 automatically (see [infrastructure](#infrastructure)).


### Black

We use [black](https://black.readthedocs.io/en/stable/) to automatically configure our code to adhere to PEP8. Black can be used in two ways:

1. Command line: navigate to the Flo Rida directory in a console and type

```bash
black {source_file_or_directory}
```

2. Editor: black can be [configured](https://test-black.readthedocs.io/en/latest/editor_integration.html) to automatically reformat a python script each time the script is saved in an editor.

If you want to use black in your editor, you may need to change the max line length in your editor settings.

Even when code has been formatted by black, you should still make sure that it adheres to the PEP8 standard set by [Flake8](#flake8).

### Naming

Naming is hard. In general, we aim for descriptive class, method, and argument names. Avoid abbreviations when possible without making names overly long, so `mean` is better than `mu`, but a class name like `MyClass` is fine.

Class names are CamelCase, and start with an upper case letter, for example `MyOtherClass`. Method and variable names are lower case, and use underscores for word separation, for example `x` or `iteration_count`.


## Dependencies and reusing code

While it's a bad idea for developers to "reinvent the wheel", it's important for users to get a _reasonably sized download and an easy install_. In addition, external libraries can sometimes cease to be supported, and when they contain bugs it might take a while before fixes become available as automatic downloads to Flo Rida users.
For these reasons, all dependencies in Flo Rida should be thought about carefully, and discussed on GitHub.

Direct inclusion of code from other packages is possible, as long as their license permits it and is compatible with ours, but again should be considered carefully and discussed in the group. Snippets from blogs and [stackoverflow](https://stackoverflow.com/) can often be included without attribution, but if they solve a particularly nasty problem (or are very hard to read) it's often a good idea to attribute (and document) them, by making a comment with a link in the source code.


## Testing

All code requires testing. We use the [unittest](https://docs.python.org/3.3/library/unittest.html) package for our tests. (These tests typically just check that the code runs without error, and so, are more _debugging_ than _testing_ in a strict sense. Nevertheless, they are very useful to have!)

You can run the tests by typing
```bash
poetry run python -m unittest
```

Every new feature should have its own test. To create ones, have a look at the `test` directory and see if there's a test for a similar method. Copy-pasting this is a good way to start.

Next, add some simple (and speedy!) tests of your main features. If these run without exceptions that's a good start! Next, check the output of your methods using any of these [assert methods](https://docs.python.org/3.3/library/unittest.html#assert-methods).


### Debugging

Often, the code you write won't pass the tests straight away, at which stage it will become necessary to debug.
The key to successful debugging is to isolate the problem by finding the smallest possible example that causes the bug.
In practice, there are a few tricks to help you to do this, which we give below.
Once you've isolated the issue, it's a good idea to add a unit test that replicates this issue, so that you can easily check whether it's been fixed, and make sure that it's easily picked up if it crops up again.
This also means that, if you can't fix the bug yourself, it will be much easier to ask for help (by opening a bug-report issue).

1. Run individual test scripts instead of the whole test suite:
```bash
python tests/unit/path/to/test
```
You can also run an individual test from a particular script, e.g.
```bash
python tests/unit/test_quick_plot.py TestQuickPlot.test_failure
```
If you want to run several, but not all, the tests from a script, you can restrict which tests are run from a particular script by using the skipping decorator:
```python
@unittest.skip("")
def test_bit_of_code(self):
    ...
```
or by just commenting out all the tests you don't want to run
2. Set break points, either in your IDE or using the python debugging module. To use the latter, add the following line where you want to set the break point
```python
import ipdb; ipdb.set_trace()
```
This will start the [Python interactive debugger](https://gist.github.com/mono0926/6326015). If you want to be able to use magic commands from `ipython`, such as `%timeit`, then set
```python
from IPython import embed; embed(); import ipdb; ipdb.set_trace()
```
at the break point instead.
Figuring out where to start the debugger is the real challenge. Some good ways to set debugging break points are:
  a. Try-except blocks. Suppose the line `do_something_complicated()` is raising a `ValueError`. Then you can put a try-except block around that line as:
  ```python
  try:
      do_something_complicated()
  except ValueError:
      import ipdb; ipdb.set_trace()
  ```
  This will start the debugger at the point where the `ValueError` was raised, and allow you to investigate further. Sometimes, it is more informative to put the try-except block further up the call stack than exactly where the error is raised.
  b. Warnings. If functions are raising warnings instead of errors, it can be hard to pinpoint where this is coming from. Here, you can use the `warnings` module to convert warnings to errors:
  ```python
  import warnings
  warnings.simplefilter("error")
  ```
  Then you can use a try-except block, as in a., but with, for example, `RuntimeWarning` instead of `ValueError`.

### Profiling

Sometimes, a bit of code will take much longer than you expect to run. In this case, you can set
```python
from IPython import embed; embed(); import ipdb; ipdb.set_trace()
```
as above, and then use some of the profiling tools. In order of increasing detail:
1. Simple timer. In ipython, the command
```
%time command_to_time()
```
tells you how long the line `command_to_time()` takes. You can use `%timeit` instead to run the command several times and obtain more accurate timings.
2. Simple profiler. Using `%prun` instead of `%time` will give a brief profiling report
3. Detailed profiler. You can install the detailed profiler `snakeviz` through pip:
```bash
pip install snakeviz
```
and then, in ipython, run
```
%load_ext snakeviz
%snakeviz command_to_time()
```
This will open a window in your browser with detailed profiling information.

## Documentation

Flo Rida is documented in several ways.

First and foremost, every method and every class should have a [docstring](https://www.python.org/dev/peps/pep-0257/) that describes in plain terms what it does, and what the expected input and output is.

These docstrings can be fairly simple, but can also make use of [reStructuredText](http://docutils.sourceforge.net/docs/user/rst/quickref.html), a markup language designed specifically for writing [technical documentation](https://en.wikipedia.org/wiki/ReStructuredText). For example, you can link to other classes and methods by writing ```:class:`florida.Flow` ``` and  ```:meth:`add_rest()` ```.

To allow for the API documentation to be built, we add reStructuredText files to import docstrings from the source code.
If you’ve added a new class to a module, search the docs directory for that module’s `.rst` file and add your
class (in alphabetical order) to its index. If you’ve added a whole new module, copy-paste another module’s file and
add a link to your new file in the appropriate `index.rst` file.

We have also written additional documentation in separate reStructuredText files within the docs directory. This additional documentation serves as a place for new users to get started and covers topics such as installation instructions and some simple code examples.

Using [Sphinx](http://www.sphinx-doc.org/en/stable/) the documentation in `docs` can be converted to HTML, PDF, and other formats. Our documentation can be found online [here](https://shiny-chainsaw-08d8e12a.pages.github.io/)

### Building the documentation

To test and debug the documentation, it's best to build it locally. To do this, navigate to your Flo Rida directory in a console, and then type:

(Windows)
```
cd docs
.\make.bat html
```

(GNU/Linux and MacOS)
```
cd docs
make html
```
You can then open the `doc/index.html` within your browser and nagivate through the documentation to your desired page.


### Example scripts

We also include example scripts within the [examples directory](examples/). These include the major features of Flo Rida,
with the idea being that we shouldn’t have any two examples that show exactly the same thing. The features that are
considered “major” is of course wholly subjective, so please discuss on GitHub before! We want to keep the set fairly
small because examples must also be maintained.

Please follow the (naming and writing) style of existing scripts where possible


## Infrastructure

### Poetry

The installation of Flo Rida, the management of dependencies, and building are handled by [poetry](https://python-poetry.org/).

Configuration files:

```
pyproject.toml
```

This file does not need to be modified manually. Instead, new dependencies should be added using

```
poetry add <package-name>
poetry add -dev <package-name>  # if the dependency is only required for development
```

and removed using

```
poetry remove <package-name>
poetry remove -dev <package-name>  # if the dependency is only required for development
```


### Continuous Integration using GitHub actions

Each change pushed to the Flo Rida GitHub repository will trigger the test and benchmark suites to be run, using [GitHub actions](https://github.com/features/actions).

Tests are run for different operating systems, and for all python versions officially supported by Flo Rida. If you opened a Pull Request, feedback is directly available on the corresponding page. If all tests pass, a green tick will be displayed next to the corresponding test run. If one or more test(s) fail, a red cross will be displayed instead.

Configuration files for various GitHub actions workflow can be found in `.github/worklfows`.


### GitHub

GitHub does some magic with particular filenames. In particular:

- The first page people see when they go to [our GitHub page](https://github.com/northvolt/flo-rida) displays the contents of [README.md](README.md), which is written in the [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format. Some guidelines can be found [here](https://help.github.com/articles/about-readmes/).
- This file, [CONTRIBUTING.md](CONTRIBUTING.md) is recognised as the contribution guidelines and a link is [automatically](https://github.com/blog/1184-contributing-guidelines) displayed when new issues or pull requests are created.


## Releases

We use [github releases](https://github.com/northvolt/flo-rida/releases) to manage the releases of Flo Rida.
We use [semantic versioning](https://semver.org/) to assign a version number to each release. These version
numbers consist of three numbers MAJOR.MINOR.PATCH, according to:

1. MAJOR version when you make incompatible API changes,
2. MINOR version when you add functionality in a backwards compatible manner, and
3. PATCH version when you make backwards compatible bug fixes.

Between releases, we create a draft release that is updated with the latest features and bug fixes.

When we are ready to release, we build using [poetry](https://python-poetry.org/):
```
poetry build
```
and attach the build files to the release on github.

## Acknowledgements

This CONTRIBUTING.md file, along with large sections of the code infrastructure,
was copied from the excellent [Pints GitHub repo](https://github.com/pints-team/pints)
and [PyBaMM Github repo](https://github.com/pybamm-team/PyBaMM)
