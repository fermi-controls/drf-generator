# DRF Generator

The DRF generator defines a syntax for expressing many [DRF](https://cdcvs.fnal.gov/redmine/projects/drf/wiki) strings in a single string.

The syntax is inspired by Unix (bash) glob syntax, but not an exact match as glob is meant to file paths.

## Installation

```bash
pip install --user --extra-index-url https://www-bd.fnal.gov/pip3 drf_generator
```

## Features

### List

Curly brackets surrounding comma separated values define a list of strings to be included with each generated DRF string.

For example:

```bash
python drf_generator "{I,R}:VT001"
```

Generates:

```text
I:VT001
R:VT001
```

### Range

Curly brackets surrounding two values separated by a double dot (`..`) define a range of integers to be included with each generated DRF string.

For example:

```bash
python drf_generator "I:VT{000..002}"
```

Generates:

```text
I:VT000
I:VT001
I:VT002
```

### Example use in code

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

from drf_generator import generate

def main(extended_drfs):
    return generate(extended_drfs)

if __name__ == '__main__':
    print(main(sys.argv[1:]))

```

## TODOs

- Allow square bracket lists
- Define a special, non-glob, range step

## Building tarball

Make sure `setup.py` has the correct version number.

```bash
make
```

will create `drf_generator.tgz`.

## Deploying

This needs to be copied to the web server. Until this is automated, I'm copying it with the command

```bash
scp drf_generator.tgz chablis:/usr/local/www/data/pip3/drf-generator/drf_generator-VID.tgz
```

Replace VID with the current version number in `setup.py`. Make sure to tag the project, too.

```bash
git tag vVID
```

## Development

To test local modifications, use pip's editable mode.

`pip install -e .`
