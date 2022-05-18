# rMATS-turbo_NP
Source code and Supplemental data related to the rMATS-turbo manuscript
## Figure 3
  - Source code for generating Figure 3 is demonstrated in `plot_Fig_PC3E_GS869.ipynb`
  - Input files for generating Figure 3 is located in folder `PC3E-GS689`
## Figure 4
  - Source code for generating Figure 4 is demonstrated in `plot_Fig_CCLE.ipynb`
  - Input files for generating Figure 4 is located in folder `CCLE`
## Requirements
  - Jupyter Notebook
  - [rmats2sashimiplot](https://github.com/Xinglab/rmats2sashimiplot)
  - Python related dependencies:
    - rpy2
  - R packages
    - zeallot
    - [ComplexHeatmap](https://www.bioconductor.org/packages/release/bioc/html/ComplexHeatmap.html)
    - circlize
    - ggplot2
    - ggrepel

## Install

* install most dependencies to a conda environment
  + `conda create --prefix ./conda_env`
  + `conda activate ./conda_env`
  + `conda install -c conda-forge -c bioconda --file ./conda_requirements.txt`
  + `CFLAGS="-I$(pwd)/conda_env/include" pip install rpy2==2.8.6`
  + `conda deactivate`
* install rmats2sashimiplot and samtools to a separate environment
  + For some reason there is a dependency conflict when trying to install everything in 1 environment
  + `conda create --prefix ./conda_env_rmats2sashimiplot`
  + `conda activate ./conda_env_rmats2sashimiplot`
  + `conda install -c conda-forge -c bioconda --file ./conda_requirements_rmats2sashimiplot.txt`
  + `conda deactivate`

## Run

* The code can be run with the main conda_env
  + `conda activate ./conda_env`
* Convert notebooks to scripts
  + `jupyter nbconvert --to python ./plot_Fig_PC3E_GS869.ipynb`
  + `jupyter nbconvert --to python ./plot_Fig_CCLE.ipynb`
* For the PC3E notebook, the existing rmats2sashimiplot output needs to be moved to avoid an error message due to files already existing. Also the rmats2sashimiplot executable from `conda_env_rmats2sashimiplot` needs to be added to the `PATH`
  + `mv ./PC3E-GS689/plot_rmats2sashimi/output_example ./PC3E-GS689/plot_rmats2sashimi/original_output_example`
  + `PATH="$(pwd)/conda_env_rmats2sashimiplot/bin:$PATH" ipython ./plot_Fig_PC3E_GS869.py`
  + It may exit with an error message like "Aborted (core dumped)", but the output files are created in `./PC3E-GS689/plot_rmats2sashimi/output_example/Sashimi_plot/`
* For the CCLE notebook:
  + `ipython ./plot_Fig_CCLE.py`
  + The output is `./CCLE/plot_heatmap/plot_heatmap_sortedByEMT_usingCorrelation.pdf`


## TODO

* rename `plot_Fig_PC3E_GS869.ipynb` to `plot_Fig_PC3E_GS689.ipynb`
* maybe put version numbers for dependencies in the README
* In `plot_Fig_PC3E_GS869.ipynb`, the section for panel d and e shows rmats2sashimiplot printed output, but there is no plot
* maybe zip all the files in `./PC3E-GS689/rmats/post/` into a single .zip instead of just zipping a few separately
* `./plot_Fig_PC3E_GS869.ipynb` has code for generating other plots (pie, volcano) but they don't get saved to a file. Maybe update the notebook to save the output file?
