# Docker Image for NVIDIA SDK Manager

## Description

- Use Docker to create the NVIDIA SDK Manager environment
- SDK Manager version: 2.0.0-11402

## Requirements

- x86_64 or aarch64 host
- Ubuntu 18.04 or 20.04 or 22.04

## Preparation

- Install Docker
- Download `sdkmanager_2.0.0-11402_amd64.deb` from https://developer.nvidia.com/sdk-manager and put it here
- Download [google-chrome-stable_current_amd64.deb](https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb) and put it here

## Build

- `./build_x86_64`

## Run

- `./run_nv_sdk_mgr`

## Restrictions

- Both x86_64 and aarch64 host can build the image but only x86_64 host can flash the image to board

## Known Issues

- Docker container may not recognize the board so it is recommended to run the flash process in the host machine

## Usage

### Flash Jetpack 5.1.2 Linux for Jetson AGX Xavier

- _(on x86_64 host)_
  - `./build_x86_64`
  - `./run_nv_sdk_mgr`
- _(in container)_
  - `sdkmanager --cli --action install --login-type devzone --product Jetson --target-os Linux --version 5.1.2 --target JETSON_AGX_XAVIER_TARGETS --license accept`
  - Select `Skip`
  - Select `Exit`
  - `exit`
- _(on x86_64 host)_
  - `cd ~/nvidia/nvidia_sdk/JetPack_5.1.2_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra/`
  - Connect the board to host machine
  - `sudo ./flash.sh jetson-xavier mmcblk0p1`
