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

 4. Run the timed compilation. The results will be logged in `time-compile.*`.
    It will consume around 8 Gb disk when `RM_WORK="1"`, or around 18 Gb if
    `RM_WORK` is not enabled (see `compile` for settings).

 ```
    ./compile
 ```

It can be worth running the test (step 4) multiple times to see if system caching
makes any difference. To rerun, please run `./clean` and then rerun the
compilation with `./compile`.

Finally, `./distclean` can be used to remove everything.

---

# Results

Here are some results from my own testing:

### DL380 Virtual

**System:** HP DL380, 16 CPU E5-2637 v2 @3.5GHz, 128 GB RAM. Running MS Server 2012 with HyperV. Guest running Ubuntu, 80GB RAM, 16 CPU. Dedicated PHY access to SSD storage device.

  ```
  # Standard compilation
  15185.56user 1659.29system 29:37.33elapsed 947%CPU  (2017-12-15)
  15119.29user 1640.76system 29:23.00elapsed 950%CPU  (2017-12-15)
  
  # rm_work disabled
  14684.79user 1578.54system 28:56.96elapsed 936%CPU  (2017-12-14)
  14709.04user 1526.15system 30:24.63elapsed 889%CPU  (2017-12-14)

  # Using tmpfs
  15447.03user 1677.42system 26:17.88elapsed 1085%CPU  (2018-01-03)
  15720.32user 1765.11system 32:19.13elapsed 901%CPU   (2018-01-03)

  # Using tmpfs, rw_work disabled
  14878.02user 1575.68system 25:35.92elapsed 1071%CPU  (2017-12-15)
  14877.92user 1584.26system 25:39.91elapsed 1069%CPU  (2017-12-15)
  ```

### Lenovo W530

**System**: Lenovo W530 laptop. i7-3820QM CPU @2.7 GHz (4 cores x2 HT), 8 GB memory. Intel 520 SSD.

  ```
  # Standard compilation
  16426.48user 1210.09system 45:43.44elapsed 642%CPU  (2018-01-03)
  16219.27user 1193.68system 44:24.72elapsed 653%CPU  (2018-01-03)

  # rm_work disabled
  15370.77user 1107.08system 41:22.29elapsed 663%CPU
  15792.09user 1142.44system 42:55.50elapsed 657%CPU

  # Enforced limitation of 4 CPUs
  15425.47user 1165.22system 46:03.35elapsed 600%CPU  (2018-01-03)

  # VirtualBox Ubuntu guest on Ubuntu host. 4096Mb, 4 CPU
  10724.01user 1482.69system 1:03:15elapsed 321%CPU  (2018-01-03)
  10888.51user 1500.76system 1:04:04elapsed 322%CPU  (2018-01-03)
  ```
---

2018-01-02 Svein Seldal <sveinse@seldal.com>
