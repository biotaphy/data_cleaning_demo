# data_cleaning_demo
A demo for occurrence data cleaning

## Summary

The purpose of this demo is to show how someone could "clean" an occurrence dataset so
that it can be used in some analysis like species distribution modeling.  This demo is
packaged as a Docker container so that it can easily be used in a number of different
environments without the extra tasks associated with installation.

## Setup Steps

Before we can run the demo, we need to build the container.  This documentation
assumes that Docker has been installed for your environment 
(see: https://docs.docker.com/get-docker/).

1. Clone the repository

  `git clone https://github.com/biotaphy/data_cleaning_demo.git`
  
2. Change to the repository directory

  `cd data_cleaning_demo`

3. Build the docker image

  `docker build docker/ -t dc_demo`

## Run the data cleaning script

1. Run a bash shell in the container interactively

Unix:
  `docker run -v "$(pwd)"/data:/demo -it dc_demo bash`

Windows:
  `docker run -v %cd%/data:/demo -it dc_demo bash`
  
2. Run the data cleaning example from the container

  `# clean_occurrences /demo/heuchera.csv /demo/clean_data.csv /demo/wrangler_conf.json`
  
