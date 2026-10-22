# ProGlove SDK

This repository hosts the ProGlove SDK and driver, with the ProWristCam SDK
that goes with the glove. There is one product line per branch. `main`
carries no code: pick the line that matches your glove and clone that branch.

| Product line | Branch | Gloves | Status |
|---|---|---|---|
| ProGlove Gen1 | `release/gen1` | `PRO-G01` | maintenance |
| ProGlove Gen2 | `release/gen2` | `PRO-G02` | current |

A `PRO-G01` glove reflashed with Gen2 firmware becomes a `PRO-G02` and moves
to the Gen2 line. The serial on the glove's label names its line.

## Get a line

```bash
git clone --branch release/gen2 --single-branch https://github.com/Proception-AI/proglove-sdk.git
# or
git clone --branch release/gen1 --single-branch https://github.com/Proception-AI/proglove-sdk.git
```

Already cloned? `git fetch origin && git checkout release/gen2`.

## Releases

Every release is a tag named `<line>/<sdk-version>`:

```bash
git tag -l 'gen2/*'            # releases of the Gen2 line
git tag -l 'gen1/*'            # releases of the Gen1 line
git checkout gen2/<version>    # pin to one
```

Each branch has its own README and MANIFEST.txt for that line.

## Support

- Email: contact@proception.ai
- [LICENSE](LICENSE)
