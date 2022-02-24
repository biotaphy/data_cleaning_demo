# data_cleaning_demo
A demo for occurrence data cleaning

## Summary

The purpose of this demo is to show how someone could "clean" an occurrence dataset so
that it can be used in some analysis like species distribution modeling.  This demo is
packaged as a Docker container so that it can easily be used in a number of different
environments without the extra tasks associated with installation.

## Data Cleaning

For this demo, we will clean a set of occurrence records for Heuchera species.  The
original data includes 11,490 records and is a CSV file that includes species name,
decimal latitude, and decimal longitude.  To clean this dataset, we will first remove
any records that have less than four decimal places of precision.  For this scenario,
we will assume that these records will be used for creating a species distribution
model and thus, records with identical latitude and longitude values for a species
are redundant and will be removed.  Finally, we only want to create models for species
with at least 12 points, so any species that have less than 12 points will be removed.

## Setup Steps

Before we can run the demo, we need to build the container.  This documentation
assumes that Docker has been installed for your environment 
(see: https://docs.docker.com/get-docker/).

1a. Clone the repository

  `git clone https://github.com/biotaphy/data_cleaning_demo.git`

1b. Download the repository from GitHub (without using git)

  If you don't have git installed, you can download the repository as a zip file.
  Navigate to https://github.com/biotaphy/data_cleaning_demo/releases/latest and
  download the source code under the Assets section.  After download, uncompress
  the file.

2. Change to the repository directory

  `cd data_cleaning_demo`

3. Build the docker image

  `docker build docker/ -t dc_demo`

## Run the data cleaning script

1. Run a bash shell in the container interactively

Mac / Linux:
  `docker run -v "$(pwd)"/data:/demo -it dc_demo bash`

Windows:
  `docker run -v %cd%/data:/demo -it dc_demo bash`
  
2. Run the data cleaning example from the container

  `# clean_occurrences -r /demo/cleaning_report.json /demo/heuchera.csv /demo/clean_data.csv /demo/wrangler_conf.json`
  
3. From your local machine, inspect the original and cleaned occurrence data files
   (data/heuchera.csv and data/clean_data.csv).  The fields have not changed between the
   two files, but the cleaning step removed all records with less than 4 decimal places
   of precision, any duplicate points (where species name, latitude, and longitude are
   the same), and any species with less than 12 points.  The result is a cleaned dataset
   with 6678 occurrence records down from the original 11,490.  You can see a more
   detailed report of how many points were removed by each filter in the file
   `data/cleaning_report.json`.  It should contain something like the following.

```
{
    "input_records": 11489,
    "output_records": 6677,
    "wranglers": {
        "decimal_precision_filter": {
            "removed": 2978
        },
        "unique_localities_filter": {
            "removed": 1800
        },
        "minimum_points_filter": {
            "removed": 34
        }
    }
}
```
