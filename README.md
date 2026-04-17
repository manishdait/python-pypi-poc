# python-pypi-poc

Proof of concept package for a signed PyPI release workflow.

## Local build

```bash
uv sync --group build
uv run python generate_proto.py
uv build
```

## Release workflow

Pushing a tag that matches `v*.*.*` triggers [.github/workflows/publish.yml](/Users/daniel/projects/hiero/python-pypi-poc/.github/workflows/publish.yml).

The workflow:

- installs build dependencies with `pip`
- builds the wheel and sdist with `python -m build`
- signs the distributions with Sigstore
- publishes to PyPI with GitHub OIDC
- uploads the signed artifacts to the GitHub release

Local development stays on `uv`; CI release publishing uses `pip`.

The workflow currently targets the `hl-sdk-py-lin-md` runner label, matching the Python SDK workflow it was modeled after.
