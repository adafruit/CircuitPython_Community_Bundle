# CircuitPython Community Library Bundle

[![Doc Status](https://readthedocs.org/projects/circuitpython/badge/?version=latest)](https://circuitpython.readthedocs.io/en/latest/docs/drivers.html) [![Discord](https://img.shields.io/discord/327254708534116352.svg)](https://adafru.it/discord)

![Blinka Community](https://github.com/adafruit/CircuitPython_Community_Bundle/blob/main/adafruit_circuitpython_community_bundle_100_large.png)

This repo bundles a bunch of useful CircuitPython libraries into an easy to
download zip file. CircuitPython boards can ship with the contents of the zip to
make it easy to provide a lot of libraries by default.

# License
Each included library has its own license that must allow for redistribution. To
save space, license text is not included in the bundle. However, a link to each
individual repository is which should provide source code access and license
information.

# Use
To use the bundle download the zip (not source zip) from the
[latest release](https://github.com/adafruit/CircuitPython_Community_Bundle/releases/latest),
unzip it and copy over the subfolders, such as `lib`, into the root of your
CircuitPython device. Make sure to indicate that it should be merged with the
existing folder when it exists.

# Development

After you clone this repository you must run `git submodule init` on update
also do `git submodule update`.

## Updating libraries
To update the libraries run `update-submodules.sh`. The script will fetch the
latest code and update to the newest tag (not master).

## Expectations for Library Inclusion
You're interested in having your library included in the Community Bundle? Great! Here are some things to keep in mind:

 * The subject and content of your library has to be compatible with the [Adafruit Community Code of Conduct](CODE_OF_CONDUCT.md)
 * Tagged release of the library must be compatible with [circuitpython-build-tools](https://github.com/adafruit/circuitpython-build-tools). The best way to ensure this is to use Github Actions with files like those produced by our [Cookie Cutter](https://github.com/adafruit/cookiecutter-adafruit-circuitpython/)
 * If your library has a problematic release that impacts Community Bundle releases, you will do your best to resolve it in a timely manner
 * If future changes to circuitpython-build-tools impact your library, you will do your best to resolve it in a timely manner (we try to keep breaking changes to a minimum, but they do happen!)

If a particular library is causing problems for distribution in the Community Bundle we may temporarily drop it or hold it at an old revision, so that we can continue making Community Bundle releases.

## Adding a library
Determine the best location within `libraries` for the new library and then run:

    git submodule add <git url> libraries/<target directory>

The target directory should omit any MicroPython or CircuitPython specific
prefixes such as `CircuitPython_` to simplify the listing.

You should make sure that the git url has the format `https://github.com/{:user}/{:repo}.git`,
such as `https://github.com/tannewt/CircuitPython_Example.git`.  Other forms may interfere with
adabot scripts (see https://github.com/adafruit/adabot/issues/145 for details).

The repository must have a tag, as the bundle release process pulls the latest tag, usually
matching a release of your library. The tag must follow the Semver format (such as *1.2.3*).

The [circuitpython_community_library_list.md](circuitpython_community_library_list.md) page is
manually updated. Please add your library to the list with the relevant links to the repository,
pypi page and documentation if available.

## Removing a library
Only do this if you are replacing the module with an equivalent:

    git submodule deinit libraries/<target directory>
    git rm libraries/<target directory>

## Building the bundle
To build this bundle locally you'll need to install the
`circuitpython-build-tools <https://github.com/adafruit/circuitpython-build-tools>`_ package.

    python3 -m venv .env
    source .env/bin/activate
    pip install circuitpython-build-tools

Once installed, make sure you are in the virtual environment:

    source .env/bin/activate

Then run the build:

    ./build.sh
