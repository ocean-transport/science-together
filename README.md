# Science Together - How to design and execute a collaborative research project

This repository is meant as an evolving guide/log of the collaborative research untertaken within the [Climate Data Science Lab (CDSLab)](https://medium.com/pangeo/announcing-the-climate-data-science-lab-funded-by-the-moore-foundation-4bc4314ac02d).

We hope that this living document can serve as inspiration to other groups, who want to try to try alternative ways of conducting science, and hope that a variety of feedback will continously improve it.

## Why?

TBW
<!-- So what is wrong with the current way of doing research? 

Most research (at least in broader climate science), is conducted mostly in isolation. This means that  -->


## How? 

To execute a collaborative project we need to define how to organize the main components of a research project: Work and Code/Data

The *Work Structure* determines when to have meetings, what to define as milestones and as a bonus how to celebrate successful milestones.
The *Code/Data Structure* sets rules on how data needed for the particular project is generated, processed, and checked.

## Work Structure

TBW

## Code/Data Structure

We believe that most modern science projects consist at the core out of [code](https://www.chronicle.com/article/the-scientific-paper-is-outdated/?cid=gen_sign_in) which generates and analyzes data.

The basic building blocks of a 'science project' in this context are:
1. Data
2. Code
3. Publications (paper, blogpost, report)

Lets start with a very simplistic project

<img src="https://i.imgur.com/1WPVg0j.png" alt="drawing" width="150"/>

In this case the code in the repository generates some figures from the data, combines it with some text and we have a paper 🤗.

The reality of most science projects is not that simple. In many cases to get to a published result, projects depend on several datasets, require heavy processing (often creating intermediate data in the process) until the final paper can be written up. Furthermore these intermediate data might actually be used in several papers. It is thus useful to separate the concept of a 'paper'-repository from a 'project'-repository:
<img src="https://i.imgur.com/lWfM3J6.png" alt="drawing" width="600"/>

These two types of repositories have very different requirements:

- The 'paper' repository should be lightweight code to produce figures, and compile a document from these figures. Ideally this repository could be sent to a journal as is, and would be fully reproducible from the reduced data genearted in the 'project' repo. This repository does not necessarily need to contain all the bells and whistles of a python package.
- The 'project' repository is the main workhorse of a scientific project. This repository needs to contain organized, reproducible pipelines to transform the raw data into the output needed to produce the figures in the 'paper' repo.

### How to build a 'project' repository (WIP)

> We assume that all 'raw' data in this project is already [ARCO]() data. Working with local files on a supercomputer likely leads to different requirements, which we will not consider here.

The key task of the project repo is to represent and execute some sort of pipeline which transforms data in one or more stages (steps). 

There are a variety of workflow 'engines' available. Let's try to outline our requirements and make an informed decision about which system best suits our needs.

#### Feature wishlist
- Reproducible Processing Pipeline.
- Compute only when necessary.
Basically we need two types of triggers that lead to a recomputation of any target:
  - Data based triggers: E.g. if a target store is not available (or doesnt fulfil some quality control) it needs to be regenerated.
  - If anything in the code that produces the target store is changed it needs to get reproduced. Ideally this would detect any imported modules, and check these for changes too. If that is not possible we need to somehow prohibit imports...
- 'CI for data' - run automated checks on the data produced.
- Easily reproduce an older stage of the pipeline, e.g. for debugging.
- Agnostic to the choice of cloud storage/compute used.
- Versioning
This is trivial for the code, since we will use git for all of our development. **But how can we tie stored data to e.g. a certain commit of the repo**?

#### Cornerstones

- We do not want to use notebooks in our pipeline. Notebooks can be used for exploration and final visualization, but any code that enters the actual pipeline, needs to be refactored into modules/scripts.

#### Possible workflow tools

- Manually setting up github actions
- Snakemake
- Prefect
- Xarray-Beam
- ...
