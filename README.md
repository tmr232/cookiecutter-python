# Cookiecutter Python

A [Cookiecutter](https://cookiecutter.io) template for my own projects.

This is based on how I currently configure my Python projects.
You're free to use it, but I may change it on a whim.


## Dependency & Environment Management

[Poetry](https://python-poetry.org/) is used for dependency and environment management.

I find it more straight-forward than [Hatch](https://hatch.pypa.io/latest/),
and I really value the lock files.
Knowing that what you run locally is what runs in your CI is priceless.

## Testing

### Pytest

[Pytest](https://pytest.org) is my test framework of choice.

### Coverage.py

The configuration covers both code & tests.
This is because [You should include your tests in coverage](https://nedbatchelder.com/blog/202008/you_should_include_your_tests_in_coverage.html).

It also outputs to XML, for use with [Codecov.io](https://codecov.io).

## Linting & Formatting

The following tools are used:

- [Ruff](https://beta.ruff.rs/docs/)
- [isort](https://pycqa.github.io/isort/)
- [Black](https://black.readthedocs.io/en/stable/)
- [mypy](https://mypy-lang.org/)


## Automation

[Nox](https://nox.thea.codes) is used to automate everything.

Both the CI stuff, and everything else that might be needed.

If you're a tox user, read Hynek Schlawack's [Why I Like Nox](https://hynek.me/articles/why-i-like-nox/).

### No pre-commit hooks

I don't like pre-commit hooks.

If one should "commit early, commit often",
committing should Just Work™️.
Additionally, you probably don't wanna run your tests in a pre-commit hook.
So enforce in the CI, and use `nox` explicitly on your own machine.

I just run `nox` to format, lint, and test.

## GitHub CI

### Tests

`.github/workflows/tests.yml`

Run linters & tests on a matrix of OSs and Python versions.

Collect all results into a single job to be used in branch-protection rules.

Additionally, pushes coverage test results to [Codecov.io](https://codecov.io).
The metadata here is a bit messy still.
Improvements are welcome.

### Publish

`.github/workflows/publish.yml`

Uses [Trusted Publishers](https://docs.pypi.org/trusted-publishers/)
to push tagged releases to PyPI.