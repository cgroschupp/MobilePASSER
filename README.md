MobilePASSER
============

MobilePASSER is a reimplementation of the MobilePASS client in Python 3.

Installation
------------

Requires Python 3.11 or newer and [uv](https://docs.astral.sh/uv/).
The project defaults to Python 3.13 via `.python-version`.

```sh
uv sync --locked
uv run mobilepasser --help
```

Dependencies are defined in `pyproject.toml` and pinned in `uv.lock`.
uv manages the Python interpreter and the local `.venv` environment.

To install the command independently of the project environment:

```sh
uv tool install .
mobilepasser --help
```

Usage
-----

```text
usage: mobilepasser [-h] [-c CONFIG_FILE] [-k ACTIVATION_KEY] [-x INDEX] [-p POLICY]
                    [-l OTP_LENGTH] [-a]

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG_FILE, --config-file CONFIG_FILE
                        Path to the configuration file.
  -k ACTIVATION_KEY, --activation-key ACTIVATION_KEY
                        The string the MobilePass client generated.
  -x INDEX, --index INDEX
                        The index of the token to generate.
  -p POLICY, --policy POLICY
                        Policy for the token.
  -l OTP_LENGTH, --otp-length OTP_LENGTH
                        Length of the returned OTP.
  -a, --auto-update-index
                        Automatically bump the index by 1 and save to config
                        file.
```

```sh
uv run mobilepasser -k YOUR_ACTIVATION_KEY -x 0
uv run mobilepasser -c ~/.mobilepasser.cfg
```

`uv run python -m mobilepasser` and `uv run python cli.py` also work.

Configuration
-------------
The configuration file is read from `~/.mobilepasser.cfg`. Copy
`examples/mobilepasser.cfg` there and replace the example activation key with
your own. Existing configuration files remain compatible.

Command-line values override configuration values, including index `0` and an
empty policy (`-p ''`). Without a configuration file, the defaults are index `0`,
an empty policy, six OTP digits and no automatic index update.

Set `auto_update_index = True` or pass `-a` to save the next index after token
generation. If the file does not exist, `-a` creates it with the next index;
an activation key supplied on the command line is not saved to the file.

Development
-----------

Run the regression tests and build the package:

```sh
uv run python -m unittest discover -s tests -v
uv build
```
