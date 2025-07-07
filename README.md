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
   OR
   ```bash
   git clone git@github.com:gvbhalerao591/applyGDC.git
   ```

4. Create and activate a conda environment:
   ```bash
   conda create --prefix=$PWD/gradunwarp-env
   ```
   ```bash
   conda activate $PWD/gradunwarp-env
   ```

6. Install required packages:
   ```bash
   conda install pip
   ```

7. Install the gradunwarp tool:
   ```bash
   cd gradunwarp
   pip install .
   ```

8. Automatically activating the environment once you open the terminal:

   If you expect to run GDC correction regularly on new images, then it might be a good idea to add this to your environment depending upon your OS, you can add the conda activate command above to either your ~/.bashrc (Linux) or ~/.zshrc (Mac). For example, in Mac, open the terminal and type:

    ```bash
    nano ~/.zshrc
    ```
    This will open the editor in the same terminal, then go to the end of the file and write the activate command. Please note that if you created a conda environment at a specific location,n then you will have to provide the full path to the environment.
   
   ```bash
   conda activate <path/to/environment>/gradunwarp-env
   ```
   Then close this file using control+X and accept the changes. Source this file so that these changes are activated.

   ```bash
   source ~/.zshrc
   ```
   Close this terminal and open a new terminal where you should now see the gradunwarp-env automatically activated.
   
### Getting the GDC scripts

Clone this repository to get the GDC scripts:
```bash
git clone https://github.com/gvbhalerao591/applyGDC.git
```

## Usage

### Running the GDC correction

You will need coeff.grad file for running the correction. Once you have access to this file, copy this into the cloned "applyGDC" directory (or if this file is saved elsewhere, you can also provide the path to this file in Step 3 below in the "--coeff" argument). Assuming your scan (to be GDC corrected) is in a directory named 'sample01' and the filename is 'T1_orig.nii.gz', follow these steps:

1. Export the main scripts directory:
   ```bash
   export BB_BIN_DIR=$PWD/applyGDC
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

- GDC Corrected MRI scan (`T1_orig_ud.nii.gz`)
- Warp field (`T1_orig_ud_warp.nii.gz`)

## Dependencies

- conda
- Python
- gradunwarp
