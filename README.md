# Tensorflow macOS binary

  Tensorflow macOS binary, compiled with SSE4.1, SSE4.2 and AVX optimizations. 

  If you want to compile your own binary for macOS, check out [compiling your own binary](#compiling-your-own-binary)

## Getting Started

  These instructions will get you a copy of the tensorflow running with SSE4.1, SSE4.2 and AVX enabled for optimizations.
  
  Please **DO NOT** install the following binary if your CPU does not support the above optimizations.

### How do I check for compatibility?

  You should get the following warnings while running tensorflow which was downloaded through pip:

  ```
  The TensorFlow library wasn't compiled to use SSE4.1/SSE4.2/AVX instructions, 
  but these are available on your machine and could speed up CPU computations.
  ```

  If this is not something that you see while executing tensorflow programs, please do not install this binary.

### Installing

  Download the binary from the git repository

  ```
  git clone https://github.com/Thunderbottom/Tensorflow-macOS-binary.git
  ```

  Open up your existing virtualenv:

  ```shell
  source /path/to/virtualenv/bin/activate
  ```

  Or create a new one:

  ```shell
  # Make sure you have virtualenv installed
  # or install it: pip install virtualenv (Use pip3 if pip is python2)
  cd /path/to/whatever && virtualenv whatever
  ```

  Install the downloaded wheel file with pip

  ```shell
  # Use pip3 for python3
  pip install filename.whl
  # If you have an existing tensorflow installation, it'll be automatically removed and replaced.
  ```

## Post installation

  We need to check if tensorflow was properly installed. To check that, run the following command:

  ```shell
  python3 -c 'import tensorflow as tf; print(tf.__version__)'
  ```

  The output should look somewhat like this:

  ```
  1.2.0-rc0
  ```

## Built With

  * [Bazel](https://bazel.build/versions/master/docs/install.html)
  * [Xcode CommandLineTools](https://developer.apple.com/xcode/)

## Versioning

  Latest available tensorflow version: ```1.2.0-rc0```

## Compiling your own binary

  To compile your own version of tensorflow binary, you'll need the following:

  python
  ```shell
  brew install python python3
  ```
  pip
  ```shell
  # pip will probably be installed along with python
  # if pip is not installed, you may go to
  https://pip.pypa.io/en/stable/installing/
  ```
  numpy1.12.1
  ```shell
  pip install numpy
  ```
  wheel
  ```shell
  pip install wheel
  ```
  bazel - 
  ```
  https://bazel.build/versions/master/docs/install-os-x.html
  ```
  xcode commandlinetools - 
  ```shell
  # Run the following command in terminal
  xcode-select install
  ```

  Create a virtualenv - 
  ```shell
  # Make sure you have virtualenv installed
  # or install it: pip install virtualenv (Use pip3 if pip is python2)
  cd /path/to/whatever && virtualenv whatever
  ```
  
  Open the virtualenv -
  ```shell
  source /path/to/whatever/bin/activate
  ```
  
  Clone the tensorflow repository - 
  ```shell
  # Replace <latest-version> with latest revision branch from repo
  git clone https://github.com/tensorflow/tensorflow && cd tensorflow && git checkout <latest-version>
  ```
  
  Run the configuration file and configure according to your needs -
  ```shell
  ./configure
  ```
  
  After the configuration is complete, we will compile the binary -
  ```shell
  # the following command will enable SSE4.1, SSE4.2 and AVX
  bazel build -c opt --copt=-mavx --copt=-msse4.1 --copt=-msse4.2  -k //tensorflow/tools/pip_package:build_pip_package
  ```
  
  If you wish to tune the flags, or add more compilation flags,
  you may do so by adding the following flags before the `-k` flag :
  
  **CUDA** -  `--config=cuda`
  
  **AVX2** -  `--copt=-mavx2`
  
  **FMA**  - `--copt=-mfma --copt=-mfpmath=both`
  
  After the compilation is complete, we will generate the wheel file - 
  ```shell
  bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
  ```
  
  Now, the wheel file will be generated and stored at /tmp/tensorflow_pkg
  
  To install :
  ```shell
  # Use pip3 for python3
  pip install /tmp/tensorflow_pkg/filename.whl
  ```
  
  Check out [post-installation](#post-installation) instructions to check the installed binary
  
  
  
