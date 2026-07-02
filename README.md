# container-structure-test

Python wheels for [GoogleContainerTools/container-structure-test](https://github.com/GoogleContainerTools/container-structure-test),
built with [go-to-wheel](https://github.com/simonw/go-to-wheel) and published to
[PyPI](https://pypi.org/project/container-structure-test/).

```console
pip install container-structure-test
# or
uvx container-structure-test --help
```

## Releasing

Releases are driven by the [main workflow](.github/workflows/main.yaml): trigger it
from the Actions tab and enter the upstream release tag to build (e.g. `v1.22.1`).
The workflow clones upstream at that tag, cross-compiles wheels for all supported
platforms, publishes them to PyPI via trusted publishing, and creates a GitHub
release on this repo with the sigstore-signed wheels attached.

### One-time setup

1. On PyPI, add a trusted publisher for the `container-structure-test` project:
   owner `FlavioAmurrioCS`, repository `container-structure-test`, workflow
   `main.yaml`, environment `pypi`.
2. In this repo's settings, create an environment named `pypi`.
