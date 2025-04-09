# applyGDC

Apply gradient distortion correction (GDC) to brain MRI scans

## Overview

This repository provides tools to apply gradient distortion correction to MRI scans, following a similar approach to the [UK Biobank (UKB) pipeline](https://git.fmrib.ox.ac.uk/falmagro/UK_biobank_pipeline_v_1).


## Installation Instructions

### Setting up the [gradunwarp tool](https://github.com/Washington-University/gradunwarp)

1. Create a directory for the gradunwarp tool:
   ```bash
   mkdir gradunwarp_tool
   cd gradunwarp_tool
   ```

2. Clone the gradunwarp repository:
   ```bash
   git clone https://github.com/Washington-University/gradunwarp.git
   ```

3. Create and activate a conda environment:
   ```bash
   conda create --prefix=$PWD/gradunwarp-env
   conda activate $PWD/gradunwarp_tool/gradunwarp-env
   ```

4. Install required packages:
   ```bash
   conda install pip
   ```

5. Install the gradunwarp tool:
   ```bash
   cd gradunwarp
   pip install .
   ```

### Getting the GDC scripts

Clone this repository to get the GDC scripts:
```bash
git clone https://github.com/gvbhalerao591/applyGDC.git
```

## Usage

### Running the GDC correction

Assuming your scan (to be GDC corrected) is in a directory named 'sample01' and the filename is 'T1_orig.nii.gz', follow these steps:

1. Export the main scripts directory:
   ```bash
   export BB_BIN_DIR=/path/to/bb_pipeline_tools/
   ```

2. Navigate to your sample directory:
   ```bash
   cd sample01
   ```

3. Run the GDC correction:
   ```bash
   $BB_BIN_DIR/bb_pipeline_tools/bb_GDC \
     --workingdir=./T1_GDC/ \
     --in=T1_orig.nii.gz \
     --out=T1_orig_ud.nii.gz \
     --owarp=T1_orig_ud_warp.nii.gz \
     --coeff=$BB_BIN_DIR/coeff.grad
   ```

## Required Files

- The gradient coefficient file (`coeff.grad`) must be available 
- Input MRI scan in NIfTI format (`.nii.gz`)

## Output Files

- Corrected MRI scan (`T1_orig_ud.nii.gz`)
- Warp field (`T1_orig_ud_warp.nii.gz`)

## Dependencies

- conda
- Python
- gradunwarp
