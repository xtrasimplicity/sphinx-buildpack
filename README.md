# sphinx-buildpack
Sphinx buildpack for Heroku/Dokku. (http://sphinxsearch.com/)

Please note: references to Sphinx in this repository are referring to the [Sphinx search engine](http://sphinxsearch.com), not the [documentation generator](http://www.sphinx-doc.org) for Python.

# Usage
Simply include this repository's URL in your `.buildpacks` file in your application's repository, alongside your other buildpacks. Alternatively, you can use the `BUILDPACK_URL` environment variable (Dokku, old versions of Heroku), or `heroku buildpacks:set` (Heroku).

**Example implementation - using a `.buildpacks` file**
```
https://github.com/xtrasimplicity/sphinx-buildpack.git#v3.0.1
# your other buildpacks...
```

**Example implementation - using the `BUILDPACK_URL` environment variable (Dokku)**
```
dokku config:set APPLICATION_NAME BUILDPACK_URL="https://github.com/xtrasimplicity/sphinx-buildpack.git#v3.0.1"
```

**Example implementation - using `heroku buildpacks:set`**
```
heroku buildpacks:set https://github.com/xtrasimplicity/sphinx-buildpack.git#v3.0.1
```


# Known Limitations
- **Version 2.2.11: Postgres support may be broken.**   
  I've had issues staticly linking postgres when compiling, so the binary files may require additional postgres libraries (`.so` files). If you're more comfortable than I am with this sort of thing, feel free to fork this repository, patch it and then submit a PR. Rough instructions for how I compiled mysql support can be found in the development section below.

# Versions
Specific versions of Sphinx can be deployed by specifying the appropriate tag when referencing this repository in your buildpack. Each release is tagged using the same version number as Sphinx -- i.e. prebuilt binaries for Sphinx `v2.2.11` are tagged `v2.2.11` in this repository.

As of writing, the following versions are supported:
- Sphinx version 3.0.2 with glibc 2.12 support (CentOS 6, etc) => Tag: v3.0.2-glibc2.12
- Sphinx version 3.0.2 => Tag: v3.0.2
- Sphinx version 3.0.1 => Tag: v3.0.1
- Sphinx version 2.2.11 => Tag: v2.2.11

# Development
If you would like to add a new version of Sphinx to this repository, simply download the binaries for the desired version, and extract the files.
i.e:
```
tar xvfz sphinx-3.0.1-release.tar.gz
cd sphinx-3.0.1-release
```
You can then compress them into a tarball, fork this repository, replace the path to prebuilt_binaries.tar.gz, update the `bin/compile` file and then submit a merge request with the version you're adding. If accepted, a tag matching the sphinx version will be created.
