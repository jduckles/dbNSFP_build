# Download and Format dbNSFP 

Making a Docker container for the following workflow: 

https://gist.github.com/sirselim/dcaad07523c90b46c1c0685efbc5d04e

## Usage

The script will look for the zip file `dbNSFP4.0a.zip` and will not download it again if it is already there. You can test this container's further steps by pointing it at a directory already containing `dbNSFP4.0a.zip`. 

**Note:** if you make changes to the `Dockerfile` or script, you'll need to rebuild the container.  

```
git clone https://github.com/jduckles/dbNSFP_build
cd dbNSFP_build
INPUTDIR=/data/dbSNFP # Set this to a location with 100GB+ free
docker build -t dbnsfp .
docker run -it -v ${INPUTDIR}:/data dbnsfp

```

## Changelog

* [Initial Version as Gist](https://gist.github.com/sirselim/dcaad07523c90b46c1c0685efbc5d04e)
* August 22, 2019
  - Output some amount of progress feedback
  - Read the number of threads from the cpu count in /proc/cpuinfo (so assumes linux/not MacOS, ok for inside containers).
  - I removed the -S 20G memory allocation as it won’t work gracefully on machines with less memory 
  - Using functions in the BASH script to organise things a bit better 
  - Switched to Aria2c (vs wget) so I can have 5 download channels at once (faster download). Google Drive hosting is HEAPS faster, but the URLs are craptastic. 
  - Sketching out some MD5 sum checking
  - Doing a few tests to prevent re-downloading the 25GB file, but downloading it it isn’t present
