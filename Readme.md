Heroku buildpack: Python + TA-Lib
=================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/). This also includes the TA-Lib libraries and Python wrapper for Heroku. 


Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --buildpack https://github.com/aneesh-neelam/heroku-buildpack-python-talib.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> Detected TA-Lib in requirements.txt. Downloading prebuilt binaries.
    -----> Downloading TA-Lib binaries.
    -----> Downloading TA-Lib Python wrapper.
    Searching for TA-Lib
    Best match: TA-Lib 0.4.8
    Processing TA_Lib-0.4.8-py3.4-linux-x86_64.egg
    Adding TA-Lib 0.4.8 to easy-install.pth file

    Using /app/.heroku/python/lib/python3.4/site-packages/TA_Lib-0.4.8-py3.4-linux-x86_64.egg
    Processing dependencies for TA-Lib
    Finished processing dependencies for TA-Lib
    -----> Installing dependencies using pip
           Downloading/unpacking requests (from -r requirements.txt (line 1))
           Installing collected packages: requests
           Successfully installed requests
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> (none)

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=https://github.com/aneesh-neelam/heroku-buildpack-python-talib.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root.

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug.

TA-Lib prebuilt libraries and the Python wrapper will be installed if the file `requirements.txt` has TA-Lib as a dependency. The prebuilt libraries are hosted [here](https://github.com/aneesh-neelam/talib-binaries)

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.4.1

Runtime options include:

- python-2.7.8
- python-3.4.1
- pypy-1.9 (experimental)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well.
