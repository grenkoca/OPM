# OPM
### Openslide patch manager: parallel reading/writing of patches.

## Installation: 
```
git clone https://github.com/grenkoca/OPM.git
cd OPM/
conda create -p ./venv python=3.6.5 -y
conda activate ./venv
conda install -c sdvillal openslide # this is only required for windows
pip install .
```

## Usage
To try an example:
```
python patch_miner.py -i images/example_slide.tiff -lm images/example_lm.tiff -o example -n -1
```
By default it detects tissue and extracts 1000 random patches from the included .svs file. Play with this number as well as the number of parallel threads in example.py (default patches=1000, default threads=100)
## Options
There are also a handful of useful options:
- `READ_TYPE`: either 'sequential' or 'random'. If sequential, it repeatedly takes the top-leftmost valid index until quota is met or the slide is saturated. If random, it randomly samples a patch from the valid indices until saturated or the quota is hit.

... and various other parameters such as patch size, thumbnail/valid mask scale, and masking thresholds.

## Workflow
OPM follows the following workflow:

<img src="images/opm_flowchart.png" alt="Workflow for Open Patch Miner" width="600"/>

## Project Structure
```
.
├── images
│   ├── example_lm.tiff
│   ├── example_slide.tiff
│   └── opm_flowchart.png
├── LICENSE.txt
├── opm
│   ├── config.py
│   ├── __init__.py
│   ├── patch_manager.py
│   ├── patch.py
│   └── utils.py
├── patch_miner.py
├── README.md
├── setup.cfg
└── setup.py
```

## Changelog
Nov. 17, 2020:
- Added support for mining patches from label map along with the slide.
- Updated README

Jul. 31, 2020:
- Changed `ALLOW_OVERLAP` to `OVERLAP_FACTOR`. `OVERLAP_FACTOR` is a float from 0 to 1 that is the portion of patches that are allowed to overlap. If 0, there is no overlap allowed. If 1, they are totally allowed to overlap (except for the origin pixel). 
