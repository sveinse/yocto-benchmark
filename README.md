# Simple Yocto benchmark

Use this benchmark to measure your machine's performance in building a small
Yocto image. The download and build is deterministic and should build
equally everywhere.

 1. Install git and download this from github:

 ```
    sudo apt install git
    git clone https://github.com/sveinse/yocto-benchmark.git
    cd yocto-benchmark
 ```

 2. Install the necessary host-tools. Do do this on Ubuntu, execute

 ```
    sudo ./host-install
 ```

 3. Clone and download the necessary sources. Will download 5.3 Gb from the
    net.

 ```
    ./clone
 ```

 4. Clean the build and prepare for measured compilation.

 ```
    ./clean
 ```

 5. Run the timed compilation. The results will be logged in `results.txt`.

 ```
    ./compile
 ```

It can be worth running the test (step 5) multiple times to see if system caching
makes any difference. To rerun, please run `./clean` and then rerun the
compilation with `./compile`.

Finally, use `./distclean` to remove everything.

---

2018-01-02 Svein Seldal <sveinse@seldal.com>
