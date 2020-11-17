Title:   Reproducible Science
Summary: Session 3: Reproducible Science with provenance capture, containers, computational environments
Authors: Adina Wagner
         Lennart Wittkuhn
Date:    2020


# What will this session teach me?

- The notion of a "reproducible paper", a research object that goes beyond a PDF, but includes everything that is necessary to reproduce a scientific result.
- Concepts & technology overview and short introduction to containers, computational environments. What is a container, how can a container help reproducibility, how can I get or make containers and add them to my dataset?

## Slides

You can get a PDF of the slides [here](https://github.com/datalad-handbook/course/blob/master/talks/PDFs/MPI_Berlin_03.pdf).

# Hands-on

## Hands-on 1: Write a reproducible paper (LaTeX, Python, Make & DataLad)

> Tested to work on Linux and MacOS


``datalad clone`` the repository found at [github.com/datalad-handbook/repro-paper-sketch/](https://github.com/datalad-handbook/repro-paper-sketch/)
```sh
datalad clone https://github.com/datalad-handbook/repro-paper-sketch.git
cd repro-paper-sketch
```

Check that you have all [Requirements](https://github.com/datalad-handbook/repro-paper-sketch/#requirements) installed (latexmk and Python3)

Create a virtual environment and install the Python modules in `requirements.txt` with [pip](https://pip.pypa.io/en/stable/)
```
virtualenv --python=python3 ~/env/repro
. ~/env/repro/bin/activate
pip install -r requirements.txt
```

Run ``make`` to see the template in action, and take a look into the resulting PDF (``main.pdf`` with a PDF reader).
```
make
```

Then, take a look into the script inside of ``code/`` and the ``Makefile``, and try to find out what how the setup works.
Change the color palette from "muted" to "Blues" (in the function [plot_relationships()](https://github.com/datalad-handbook/repro-paper-sketch/blob/395fe9a807f075e7ad42f2b1d55e96ecf152fa7f/code/mk_figuresnstats.py#L38)) and rerun ``make``.
Take another look into the PDF to see an updated figure.


## Hands-on 2: Run a containerized neuroimaging workflow

> Tested to work on Linux and MacOS, taken from github.com/ReproNim/containers

This short example runs a containerized neuroimaging pipeline ([MRIQC](https://mriqc.readthedocs.io/en/stable/), a pipeline for creating image quality metrics from structural and functional magnetic resonance imaging data) on fMRI data.

Source: [github.com/repronim/containers](https://github.com/repronim/containers)

Create a new dataset to contain mriqc output:
```
datalad create -d ds000003-qc -c text2git
cd ds000003-qc
```

Install the ReproNim container collection for convenience:
```
datalad install -d . ///repronim/containers
# (optionally) Freeze container of interest to the specific version desired
# to facilitate reproducibility of some older results
datalad run -m "Downgrade/Freeze mriqc container version" containers/scripts/freeze_versions bids-mriqc=0.15.1
```

Install input data as a subdataset. The dataset installed here is a slimmed-down [OpenNeuro dataset](https://github.com/OpenNeuroDatasets/ds000003) with only two subjects.
```
datalad clone -d . https://github.com/ReproNim/ds000003-demo sourcedata
```

Execute a containerized pipeline using ``datalad containers-run`` to create a re-executable run record (this takes about 15 minutes of execution time):
```
datalad containers-run \
        -n containers/bids-mriqc \
        -m "Run MRIQC on the input data" \
        --input sourcedata \
        --output . \
        '{inputs}' '{outputs}' participant group
```

Check the Git log to find the run-records commit hash:

```
git log -n 1
```
Rerun the run record (much faster execution time because we saved the work dir).

```
datalad rerun <INSERT HASH>
```
Use Git tool to explore what changed between runs (if you end up in a pager, pressing ``q`` gets you out):
```
# get difference between most recent and second most recent commit for one file
git diff HEAD..HEAD~1 -- group_bold.html

# list all files that were changed between the two runs
git diff HEAD..HEAD~1 --name-only

...
```

# Further reading, helpful links, and background information

* The Turing Way's ["Guide for Reproducible Research"](https://the-turing-way.netlify.app/reproducible-research/reproducible-research.html)
* An introduction to and tutorial to [Reproducibility with Make](https://the-turing-way.netlify.app/reproducible-research/make/make-examples.html)
* The OHBM Traintrack session on [Containerization with Docker and Singularity](https://www.youtube.com/watch?v=pc3YOZUG3lQ&feature=youtu.be) by Saskia and Steffen Bollmann
* [10 simple rules for writing Dockerfiles for reproducible data science](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008316)
* [Singularity: Scientific containers for mobility of compute](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0177459)
* [Neurodocker](https://github.com/ReproNim/neurodocker) to generate custom Dockerfiles and Singularity recipes for neuroimaging
* [repo2docker](https://github.com/jupyterhub/repo2docker) can fetch a Git repository/DataLad dataset and build a container from configuration files
* Handbook usecase [Writing a reproducible paper](http://handbook.datalad.org/en/latest/usecases/reproducible-paper.html)