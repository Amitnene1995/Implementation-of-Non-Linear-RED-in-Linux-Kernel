
# Implementation-of-Non-Linear-RED-in-Linux-Kernel
# Course Code - CS822
# Assignment No - FP7

# Overview
NLRED[2] is an extension of RED[1], that Drops packet in a quadratic fashion instead of linear as in red. That is it drops less packet when average queue length is less and more packet when average queue lenght is high. This repository provides an implementation of NLRED in the Linux kernel.
Steps to build the modified kernel with NLRED algorithm

   1. Download or clone this repository on your local machine

   2. Configure the kernel

    make menuconfig

   3. Compile the kernel

    make

   4. Build and install the modules

    make modules

    make modules_install

   5. Install the kernel

    make install

Steps to test the functionality of NLRED AQM by using Flexible Network Tester (Flent) [3]

   1. Setup a physical topology of three nodes:

    Client <---> Router <---> Server

   2. Create a separate passwordless SSH connection between client and router machines, so that Flent can collect queue statistics from the router machine

   3. Install Netserver in server machine

   4. Install Flent from github or ppa repository in client machine

   5. Install the modified kernel with NLRED algorithm in router machine

   6. Run Flent for plotting different graphs

# Syntax of the command to run Flent

./run-flent rrul -p [PLOT_NAME] -l 160 -H [SERVER_IP] --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=[ROUTER_SSH_IP] --test-parameter qdisc_stats_interfaces=[ROUTER_AQM_INTERFACE] --test-parameter upload_streams=num_cpus --test-parameter download_streams=num_cpus -t NLRED -o ~/Desktop/NLRED/test.png

PLOT_NAME - The type of graph needed

SERVER_IP - IP Address of the server

ROUTER_SSH_IP - IP Address using which ssh connection is setup with router

ROUTER_AQM_INTERFACE - Interface name of the router where AQM is installed
Example command to run Flent

./run-flent rrul -p all_scaled -l 160 -H 172.16.10.2 --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=192.168.20.2 --test-parameter qdisc_stats_interfaces=eth1 --test-parameter upload_streams=num_cpus --test-parameter download_streams=num_cpus -t NLRED -o ~/Desktop/NLRED/test.png
References

[1] Random Early Detection Gate ways for Congestion Avoidance by Sally Floyd and Van Jacobson.

[2] Nonlinear RED: A simple yet efficient active queue management scheme by Zhou Kaiyu, Kwan L. Yeung and Victor O.K at Department of Electrical and Electronic Engineering, The University of Hong Kong, CYC805, HKU, Pokfulam Road, Hong Kong, China

[3] Flent: The FLExible Network Tester (https://flent.org/)
