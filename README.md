
Building and uploading sisl wheels
==================================

We automate wheel building for [sisl](https://github.com/zerothi/sisl) using this custom github repository that builds on
the travis-ci OSX and Linux machines and the appveyor Windows machines.

**Note:** Windows builds are broken at the moment. The compilation works fine but sisl can't find the `.dll` files.

The travis-ci interface for the builds is
https://travis-ci.com/github/zerothi/sisl-wheels

Appveyor interface at
https://ci.appveyor.com/project/zerothi/sisl-wheels/

The driving github repository is
https://github.com/zerothi/sisl-wheels

How it works
============

It makes use of [multibuild](https://github.com/matthew-brett/multibuild) to generate self-contained wheels on all platforms. 
See their [README](https://github.com/matthew-brett/multibuild/blob/devel/README.rst) to get a deeper understanding on how they are generated.

All this repo does is to define the appropiate `.travis.yml` (linux and macOS) and `appveyor.yml` (windows) files that call the corresponding
multibuild scripts.

For linux and macOS builds, `config.sh` contains two hooks for the building process (which multibuild expects to find). All we do there is run pytest
to make sure that the generated wheels work in that environment. If any test fails, the wheels are not uploaded.

Triggering a build
==================

Use the `trigger_build.py` specifying the commit that you want to build from https://github.com/zerothi/sisl, like so:

```
python trigger_build.py v0.10.0
```

This will create a new tag (v0.10.0) in this repo, build the wheels for the v0.10.0 tag in sisl's repo and create a github release
where all the wheels will be uploaded.

**Note:** You need write access to this repo in order to trigger builds.

Which sisl commit does the repository build?
===============================================

The `sisl-wheels` repository will build the commit specified in the
``BUILD_COMMIT`` at the top of the ``.travis.yml`` file and ``appveyor.yml``
files.  This can be any naming of a commit, including branch name, tag name or
commit hash.

This is automatically handled by the `trigger_build.py` script.

Uploading the built wheels to pypi
==================================

To be done

