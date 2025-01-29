# Sysbench Benchmarks
 A repository of all benchmarks run using Sysbench.

# Install and Setup
The below commands are taken from (Sysbench repo)[https://github.com/akopytov/sysbench].

Quick install instructions:

- Debian/Ubuntu
  ``` shell
  curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | sudo bash
  sudo apt -y install sysbench
  ```

- RHEL/CentOS:
  ``` shell
  curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.rpm.sh | sudo bash
  sudo yum -y install sysbench
  ```

- Fedora:
  ``` shell
  curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.rpm.sh | sudo bash	
  sudo dnf -y install sysbench
  ```

- Arch Linux:
  ``` shell
  sudo pacman -Suy sysbench
  ```

## macOS

On macOS, up-to-date sysbench packages are available from Homebrew:
```shell
# Add --with-postgresql if you need PostgreSQL support
brew install sysbench
```

## Windows
As of sysbench 1.0 support for native Windows builds was dropped. It may
be re-introduced in later releases. Currently, the recommended way to
obtain sysbench on Windows is
using
[Windows Subsystem for Linux available in Windows 10](https://msdn.microsoft.com/en-us/commandline/wsl/about).

After installing WSL and getting into he bash prompt on Windows
following Debian/Ubuntu installation instructions is
sufficient. Alternatively, one can use WSL to build and install sysbench
from source, or use an older sysbench release to build a native binary.


# Running Benchmarks
See (Sysbench Usage)[https://github.com/akopytov/sysbench?tab=readme-ov-file#usage] for info on options.

## Standard Benchmarks

### CPU

Adjust threads to match system configuration. Time is in seconds.

``` shell
  sysbench --threads=4 --time=30 cpu run
  ```

### Memory

Adjust threads to match system configuration. Time is in seconds.

``` shell
  sysbench --threads=4 --time=30 memory run
  ```

### Disk IO

1. Prepare

Adjust file-num and file-total-size to match system desired benchmark. Or remove to go to defaults.

``` shell
  sysbench --file-num=64 --file-total-size=32M fileio prepare
  ```

2. Run

Adjust file-num and file-total-size to match system desired benchmark. Or remove to go to defaults.

``` shell
  sysbench --file-num=64 --file-total-size=32M --file-test-mode=rndrwfileio run 
  ```

2. Cleanup

Adjust file-num and file-total-size to match system desired benchmark. Or remove to go to defaults.

``` shell
  sysbench fileio cleanup 
  ```



# Results

## CPU

| System | CPU/GPU | Threads | Guest OS | Events Per Second | Latency [ms] (avg) | Latency [ms] (max/min) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| HPE DL360 GEN10 (PVE8 VM) | Intel Xeon Bronze 6104 | 4 | Ubuntu Server 22.04 LTS | 2317.56 | 1.73 | 4.95/1.71 |
| HPE DL360 GEN10 (PVE8 VM) | Intel Xeon Gold 6130 | 20 | Ubuntu Server 22.04 LTS | 521830 | 1.15 | 5.92/1.04 |
| HPE DL360 GEN10 (PVE8 VM) | Intel Xeon Gold 6130 | 4 | Ubuntu Server 22.04 LTS | 139133 | 0.86 | 1.67/0.83 |
| HPE DL360 GEN10 (PVE8 VM) | Intel Xeon Gold 6130 | 2 | Ubuntu Server 22.04 LTS | 71378 | 0.84 | 1.50/0.78 |

## Memory

| System | CPU/GPU | Threads | Total Memory Size [MiB] | Block Size [KiB] | Transferred Data [MiB] | Write Speed [MiB/s] | Latency [ms] (avg) | Latency [ms] (max/min) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| HPE DL360 GEN10 (PVE8 VM) | Intel Xeon Bronze 6104 | 4 | 102400 | 1 | 100762.48 | 3358.40 | 0.00 | 2.57/0.00 |