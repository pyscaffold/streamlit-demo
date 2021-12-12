[![Project generated with PyScaffold](https://img.shields.io/badge/-PyScaffold-005CA0?logo=pyscaffold)](https://pyscaffold.org/)

# streamlit-demo

Streamlit application powered by a [PyScaffold] project setup.

**Work in progress**: The idea of this repo is to demonstrate how to package a streamlit app using PyScaffold.
Since streamlit currently doesn't support apps as proper Python packages, this example is still suboptimal.
Following [Github issue](https://github.com/streamlit/streamlit/issues/4162) was created to improve the current situation.

The structure was created with:
```shell
putup --dsproject streamlit-demo -p git_overview \
      -d "Streamlit application powered by a PyScaffold project setup." \
      -u https://github.com/pyscaffold/streamlit-demo
```
then the actual code was taken from [git-overview] (MIT-licensed) and changed into a proper Python package layout.


The advantages over the original codebase are:
1. wheel file for distribution can be easily build with `tox -e build`,
2. unit tests can be easily added in the `tests` folder,
3. `extract-repo` is now a shell command (available after installation) instead of a script `repo.py`,
4. `git_overview` is a Python package that could be reused by other Python projects after installation,
5. all the [other advantages of a PyScaffold layout](https://pyscaffold.org/en/stable/features.html)...

## Installation & Running the dashboard

In order to set up the necessary environment:

1. create and activate the environment `streamlit-demo` with the help of [conda]:
   ```shell
   conda env create -f environment.yml
   conda activate streamlit-demo
   ```
   or use `environment.lock.yml` to recreate an environment with pinned dependencies.
> **_NOTE:_**  The conda environment will have streamlit-demo installed in editable mode.
> Some changes, e.g. in `setup.cfg`, might require you to run `pip install -e .` again.

2. run the dashboard with:
   ```shell
   streamlit run scripts/show_dashboard.py
   ```

3. optionally build a docker image and run it with:
   ```shell
   docker build -t local/streamlit-demo:latest .
   docker run -p 8501:8501 local/streamlit-demo:latest
   ```
   then open [https://localhost:8501](https://localhost:8501).

## Project Organization

```
├── AUTHORS.md              <- List of developers and maintainers.
├── CHANGELOG.md            <- Changelog to keep track of new features and fixes.
├── CONTRIBUTING.md         <- Guidelines for contributing to this project.
├── Dockerfile              <- Build a docker container with `docker build .`.
├── LICENSE.txt             <- License as chosen on the command-line.
├── README.md               <- The top-level README for developers.
├── docs                    <- Directory for Sphinx documentation in rst or md.
├── environment.yml         <- The conda environment file for reproducibility.
├── pyproject.toml          <- Build configuration. Don't change! Use `pip install -e .`
│                              to install for development or to build `tox -e build`.
├── scripts                 <- Entry-script `show_dashboard.py` for streamlit
├── setup.cfg               <- Declarative configuration of your project.
├── setup.py                <- [DEPRECATED] obsolete way of building and installation.
├── src
│   └── git_overview        <- Actual Python package `git-overview` with the main functionality.
│       ├── __init__.py
│       ├── dashboard.py    <- Layout-function of the actual dashboard.
│       ├── repo.py         <- Functions to download repo data.
│       └── utils.py        <- Some dashboard-related helpers
├── tests                   <- Unit tests which can be run with `pytest`.
├── .coveragerc             <- Configuration for coverage reports of unit tests.
├── .isort.cfg              <- Configuration for git hook that sorts imports.
└── .pre-commit-config.yaml <- Configuration of pre-commit git hooks.
```

This structure is in strong contrast to the original one:

```
├── app
│   ├── dashboard.py        <- Dashboard entry-point
│   ├── __init__.py
│   ├── repo.py             <- Script to download repo data
│   └── utils.py            <- Some dashboard-related helpers
├── Dockerfile
├── README.md
└── requirements.txt
```

<!-- pyscaffold-notes -->

## Note

This project has been set up using [PyScaffold] 4.1.1.post1.dev28+g075b76f and the [dsproject extension] 0.6.1.post28+g91ab61a.

[conda]: https://docs.conda.io/
[PyScaffold]: https://pyscaffold.org/
[pre-commit]: https://pre-commit.com/
[Jupyter]: https://jupyter.org/
[nbstripout]: https://github.com/kynan/nbstripout
[Google style]: http://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings
[PyScaffold]: https://pyscaffold.org/
[dsproject extension]: https://github.com/pyscaffold/pyscaffoldext-dsproject
[git-overview]: https://github.com/andodet/git-overview
