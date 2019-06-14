# Usage
```sh
# Clone Eigen
git clone https://github.com/eigenteam/eigen-git-mirror
mkdir build
cd build/

# Download the 'time-g++.sh' script - a drop in replacement
# for g++ which tracks compile times and memory usage.
wget https://raw.githubusercontent.com/bjornpiltz/compiler_profiler/master/time-g%2B%2B.sh
chmod a+x time-g++.sh

# Configuration:
# Tell CMake to use time-g++.sh as a compiler
export CXX=$(pwd)/time-g++.sh

# Tell time-g++.sh which compiler to actually use
export ACTUAL_COMPILER=/usr/bin/g++

# Note to Mac users: The built-in time tool is unusable. 
# You have to install gtime with homebrew or MacPorts.
export TIME_CMD=/usr/bin/time

# Where do you want the output?
export PROFILING_LOG=$(pwd)/eigen_compile_times_gcc.csv

# Configure the Eigen test suite
cmake ../eigen-git-mirror/

# Clear the log after calling cmake to remove some noise.
rm $PROFILING_LOG

# Now compile the test suite and wait some seven hours...
make check
```
