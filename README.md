# container-structure-test

[![PyPI - Version](https://img.shields.io/pypi/v/container-structure-test.svg)](https://pypi.org/project/container-structure-test)

-----

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

### Patches

Local fixes carried on top of upstream live in [`patches/`](patches/) and are applied
to the upstream clone, in filename order, before the build. They must be
`git format-patch` output — the build reads each patch's `Subject:` line to list the
applied patches in a banner at the top of the wheel's README, which is what PyPI
renders on the project page. The built binary also reports its version with a
`+patched` suffix (e.g. `v1.22.1+patched`); the PyPI version stays a plain `1.22.1`.
A matching `+patched` is not possible there — PyPI rejects PEP 440 local version
identifiers — and a `.postN` suffix is deliberately not used, since every wheel this
project ships is patched and there is no unpatched build to distinguish it from. The
consequence is that an upstream tag can only be published once; carrying a new patch
means building a newer upstream tag.

A patch that no longer applies fails the build rather than being skipped, so a wheel
never ships silently unpatched. When that happens, rebase the patch against the new
upstream tag and re-export it with `git format-patch`.

### One-time setup

1. On PyPI, add a trusted publisher for the `container-structure-test` project:
   owner `FlavioAmurrioCS`, repository `container-structure-test`, workflow
   `main.yaml`, environment `pypi`.
2. In this repo's settings, create an environment named `pypi`.
