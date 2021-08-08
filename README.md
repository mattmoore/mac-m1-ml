# Mac M1 ML

Using ML tools on Mac M1.


## Tensorflow

There's a lot of garbage info out there on Tensorflow on M1. Here's some solid info I've confirmed:

### Compiling on M1, using Rosetta 2

I've already compiled a version you should be able to install directly from pip using a terminal running in Rosetta 2 mode:

```shell
python3 -m pip install tensorflow-2.7.0-cp38-cp38-macosx_11_0_x86_64.whl
```

```shell
# 1.) I installed some brew packages before even installing python (notice that I am using Rosetta brew and not my default arm brew)
/usr/local/bin/brew install zlib
/usr/local/bin/brew install bzip2
/usr/local/bin/brew install sqlite
/usr/local/bin/brew install libiconv
/usr/local/bin/brew install libzip
/usr/local/bin/brew install xz

# 2.) install bazelisk
/usr/local/bin/brew install bazelisk

# 3.) switch to your Rosetta python env (I use python 3.8.5 installed with rosetta-brew's pyenv)

# 4.) clone tf repo
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow

# 5.) run configure and say No to gpu options
./configure

# 6.) build (this runs between 2 and 3 hours; 100% CPU all the time)
bazel build //tensorflow/tools/pip_package:build_pip_package

# 7.) create whl
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg

# 8.) install tf via pip
pip install /tmp/tensorflow_pkg/tensorflow-2.7.0-cp38-cp38-macosx_11_0_x86_64.whl
```

