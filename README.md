# sphinx-buildpack
Heroku buildpack for Sphinx search. (http://sphinxsearch.com/)

# Usage
Simply include this repository's URL in your `.buildpacks` file in your application's repository, alongside your other buildpacks.

# Known Limitations
- **Postgres support may be broken.**   
  I've had issues staticly linking postgres when compiling, so the binary files may require additional postgres libraries (`.so` files). If you're more comfortable than I am with this sort of thing, feel free to fork this repository, patch it and then submit a PR. Rough instructions for how I compiled mysql support can be found in the development section below.

# Versions
Specific versions of Sphinx can be deployed by specifying the appropriate tag when referencing this repository in your buildpack. Each release is tagged using the same version number as Sphinx -- i.e. prebuilt binaries for Sphinx `v2.2.11` are tagged `v2.2.11` in this repository.

As of writing, the following versions are supported:
- Sphinx version 2.2.11 => Tag: v2.2.11


# Development
If you would like to add a new version of Sphinx to this repository, simply download the source code for the desired version, configure it to use staticly-linked mysql and postgres libraries, and compile it.
i.e:
```
tar xvfz sphinx-2.2.11-release.tar.gz
cd sphinx-2.2.11-release
./configure --prefix="/home/`whoami`/sphinx_build" --with-static-mysql --with-mysql-libs=/usr/lib/x86_64-linux-gnu --with-pgsql
make -j4 install
```
You can then compress them into a tarball, fork this repository, replace the path to prebuilt_binaries.tar.gz, update the `bin/compile` file and then submit a merge request with the version you're adding. If accepted, a tag matching the sphinx version will be created.
