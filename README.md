# rrrpkg
Use of an R package to facilitate reproducible research

### What is a research compendium?

>We introduce the concept of a compendium as both a container for the different elements that make up the document and its computations (i.e. text, code, data,...), and as a means for distributing, managing and updating the collection. - Gentleman, R. and Temple Lang, D. (2004)

The goal of a research compendium is to provide a standard and easily recognisable way for organising a reproducible research project with R. A research compendium is ideal for projects that result in the publication of a paper because then readers of the paper can access the code and data that generated the results in the paper. A research compendium is a convention for how you organise your research artefacts into directories. The guiding principle in creating a research compendium is to organise your files following conventions that many people use. Following these conventions will help other people instantly familiarise themselves with the structure of your project, and also support tool building which takes advantage of the shared structure.

Some of the earliest examples of this approach can be found in Robert Gentleman and Duncan Temple Lang's 2004 paper "Statistical Analyses and Reproducible Research" [Bioconductor Project Working Papers](http://biostats.bepress.com/bioconductor/paper2/) and Gentleman's 2005 article ["Reproducible Research: A Bioinformatics Case Study"](http://dx.doi.org/10.2202/1544-6115.1034) in _Statistical Applications in Genetics and Molecular Biology_. Since then there has been a substantial increase in the use of R as a research tool in many fields, and numerous improvements in the ease of making R packages. This means that making a research compendium based on an R package is now a practical solution to the challenges of organising and communicating research results for many scientists. 

### Why create a research compendium?

Using research compendia simplifies file management and streamlines analytical workflows, making your research more efficient. A compendium makes it easier to communicate your work with other researchers (and your future self), to demonstrate the correctness of your results. This can lead to higher visibility of your work, receiving credit for code as well as the paper, a boost in citations, and allows others to more easily build on your work. 

### How to make a research compendium

 At its simplest, a research compendium might consist of a single file of R code with inline comments documenting the workflow. A slightly more complex approach might be a R markdown file with text and code in the same source document. In many cases these simple approaches will be ideal, and more elaborate organisation would add unnecessary complexity and points of failure. But many projects will require some additional organisation to make them easier to work with. An ideal organisation for a more complex project would look like this:

* A **README.md** file that describes the overall project and where to get started. It's helpful to include graphical summary of the interlocking pieces of the project.
* Script files with reusable functions go in the **`R/`** directory. This is often a small part of an analysis but it’s important.
* Raw data files live in the **`data/`** directory. If your data are very large, it may be worthwhile to include small sample dataset that so that people can try out the techniques without having to run very expensive computations
* Analysis scripts and reports files go in the **`analysis/`** directory. The `analysis/` directory could include either an R markdown file, a makefile or a makefile.R file that controls the order of the code. In many cases it will be useful to give the analysis scripts ascending names, e.g. 001-load.R, 002-clean.R etc (but this only gives a linear ordering, it doesn't capture the full tree of dependencies in the way a makefile does)
* A **DESCRIPTION** file that gives structured, machine- and human-readable information about the authors, licensing, the software dependencies and other metadata of the compendium. When a DESCRIPTION file is included along with the other items above, then the compendium is also a formal R package and you can take advantage of many time-saving tools for package development, testing and sharing (for example, the `devtools` package).

If you’re familiar with R packages, you’ll notice many similarities with these conventions. But there are some differences:

* Stand alone package vignettes are often used as the manuscript file, but may not to the best way to organise complex computation because they don’t make the ordering explicit (or give the big picture). A separate `analysis/` or `manuscript/` directory is more helpful here, and many people use a makefile to organise file dependencies
* Documentation and testing tend to be less important for compendia than packages - they are still important, but they tend to come later in the process, and are used by relatively more advanced/experienced compendia users. 

More complex research compendia include other package elements such as a licence, tests, continuous integration, and dependencies external to R, such as a dockerfile to replicate the computational environment that the analyses were originally conducted in. 

### How to share a research compendium

You should prepare your compendium using a version control system such as git. Then when you are ready to share it, the best way is to archive a specific commit of your compendium at a repository that issues permanent URLs such as [figshare](http://figshare.com/) or [zenodo](https://zenodo.org/) which give DOIs for archived files. Then you can circulate the version of your compendium that is the version that generated the published results. This means you have a publicly available snapshot of the code that matches the paper. Code development can continue after the paper is published, but with a DOI that links to a specific commit, other users of the code can be confident that they have the version that matches the paper. A DOI also simplifies citation of the compendium, so you can cite it in your paper (and others can cite it in their work) using a persistent URL. 

Putting your compendium on dropbox or google drive is another way to make the compendium easily available. 

### Getting started with a research compendium

* Start simple - it’s ok to have just one R script or one R markdown file. But as you get more complex and start to break into multiple files, that you should follow these simple conventions described above
* A simple example of a research compendium might look like this:

```
project
|- DESCRIPTION          # project metadata and dependencies 
|- README.md            # top-level description of content and guide to users
|
|- data/                # raw data, not changed once created
|  +- my_data.csv       # data files in open formats such as TXT, CSV, TSV, etc.
|
|- analysis/            # any programmatic code 
|  +- my_scripts.R      # R code used to analyse and visualise data 
```

A real-world example of this simple research compendium format is online here: https://github.com/duffymeg/BroodParasiteDescription

* An intermediate example might look like this:

```
project
|- DESCRIPTION          # project metadata and dependencies 
|- README.md            # top-level description of content and guide to users
|- NAMESPACE            # exports R functions in the package for repeated use
|- LICENSE              # specify the conditions of use and reuse of the code, data & text
|
|- data/                # raw data, not changed once created
|  +- my_data.csv       # data files in open formats such as TXT, CSV, TSV, etc.
|
|- analysis/            # any programmatic code 
|  +- my_report.Rmd     # R markdown file with R code and narrative text interwoven
|
|- R/                   #  
|  +- my_functions.R    # custom R functions that are used more than once in the project
|
|- man/
|  +- my_functions.Rd   # documentation for the R functions (auto-generated when using devtools)
```
This intermediate example includes the `R/` and `man/` directories. These contain custom functions that are used repeatedly throughout the project. The `man/` directory contains the manual, or documentation on the use of the functions. The NAMESPACE and LICENSE files are also typical features of R packages. 

For example, https://github.com/USEPA/LakeTrophicModelling has much of the repeatable code in `R/` and  the remainder of the code and text in `vignettes/manuscript.Rmd`.

* As your project becomes more complex, it's ok to add logically-named subdirectories to keep files organised. There are very few strict rules here, the key principle is to keep your compendium logically organised so that another person can easily understand how your files relate to each other without having to ask you. 

* Naming objects is notoriously difficult to do well, so it's worth to put some effort into a logical and systematic file naming convention if you have a complex project with many files and directories (for example, a multi-experiment study where each experiment has numerous data and code files). 

* A more complex research compendium might look like this:

```
project
|- DESCRIPTION          # project metadata and dependencies 
|- README.md            # top-level description of content and guide to users
|- NAMESPACE            # exports R functions in the package for repeated use
|- LICENSE              # specify the conditions of use and reuse of the code, data & text
|- .travis.yml          # continuous integration service hook for auto-testing at each commit
|- dockerfile           # makes a custom isolated computational environment for the project
|
|- data/                # raw data, not changed once created
|  +- my_data.csv       # data files in open formats such as TXT, CSV, TSV, etc.
|
|- analysis/            # any programmatic code
|  +- my_report.Rmd     # R markdown file with narrative text interwoven with code chunks 
|  +- makefile          # builds a PDF/HTML/DOCX file from the Rmd, code, and data files
|  +- scripts/          # code files (R, shell, etc.) used for data cleaning, analysis and visualisation 
|
|- R/                     
|  +- my_functions.R    # custom R functions that are used more than once throughout the project
|
|- man/
|  +- my_functions.Rd   # documentation for the R functions (auto-generated when using devtools)
|
|- tests/
|  +- testthat.R        # unit tests of R functions to ensure they perform as expected
```

Real-world examples that are similar to this more complex research compendium format are online here:

- https://github.com/cboettig/nonparametric-bayes/  
- https://github.com/benmarwick/1989-excavation-report-Madjebebe 

Note that although these real-world examples have a common basic R package structure, they show quite a bit of variation in the location of things like the dockerfile, and the use of package features like the `inst/` and `vignettes/` directories. This kind of variation does not affect the function of the compendium as a package, and largely reflects personal choices about what kind of file organisation makes the most sense to each researcher. 

### Useful tools and templates for making research compendia  

- Probably the most useful set of tools for making research compendia as R packages is the `devtools` package combined with the [RStudio](http://www.rstudio.com/) integrated development environment, and a copy of Hadley Wickham's book [R Packages](http://r-pkgs.had.co.nz/)

- Several people have developed templates for using R packages as research compendia. These templates are mostly for their personal use, and are works-in-progress, but are freely available for others to adapt and learn from:  
    + [Jeff Hollister's manuscriptPackage](https://github.com/jhollist/manuscriptPackage)  
    + [Carl Boettiger's template](https://github.com/cboettig/template)  
    + [Francisco Rodriguez-Sanchez's template](https://github.com/Pakillo/template)
    + [Ben Marwick's researchcompendium](https://github.com/benmarwick/researchcompendium)

These templates are empty packages that show various ways of organising an analysis as an R package (eg. where the manuscript is the package vignette, or similarly bundled with the package) 

-   For writing papers in R markdown, useful packages include include [captioner](https://github.com/adletaw/captioner) and [kfigr](https://github.com/mkoohafkan/kfigr) for figure and table captions and cross-referencing. There are many R markdown templates in the [rticles](https://github.com/rstudio/rticles) package, these make is easy to get started with formatting and citations to produce attractive PDF/HTML/DOCX output from R markdown documents.

- If you start with a single R markdown document and want to develop it into a package, see the [rlp](https://github.com/yihui/rlp) package, which has functions for this purpose. 

-   For capturing the computational environment of an analysis, [rocker](https://github.com/rocker-org/rocker) is a project that provides Docker containers to run R in a lightweight virtual environment. The hadleyverse container includes dplyr, ggplot2, etc., as well as RStudio server and LaTeX. The package [harbor](https://github.com/wch/harbor) provides functions for controlling docker containers on local and remote hosts. The [analogsea](https://github.com/sckott/analogsea) package has functions for deploying R and RStudio quickly & easily on DigitalOcean clusters using Docker images for cloud computing. The [dockertest](https://github.com/richfitz/dockertest) package contains functions for generating Dockerfiles from R packages and other R projects, and building Docker containers that contains all the package dependencies.

- For complex workflows where you only want to run components that have changed (eg. because of long compute times), or need to run a series of R scripts in a specific order, you may find [make](http://www.gnu.org/software/make/) useful. Make can be used to automatically execute sequences of analyses and update any set of files that depend on another set of files. This makes it a good solution for many data analysis and data management problems, including the generation of images from data. The [remake](https://github.com/richfitz/remake) package allows you to write makefile-like files entirely within R, saving you from having to learn make's language. 

### Challenges for future work

* We could do with a package like devtools that automates the common problems and handles typical research workflow issues
* We all need to try out the R package structure with our actual research projects and report back in one year so see what works, what doesn't, and where the pain points are. 
* Would be useful to share these processes in public so that people have can good examples that they can look at

### Further reading

[rOpenSci Guide to Reproducible Research](http://ropensci.github.io/reproducibility-guide/sections/introduction/)

[Gandrud C 2013 Reproducible Research with R and RStudio. CRC Press Florida](http://christophergandrud.github.io/RepResR-RStudio/)

[Gentleman, R. and Temple Lang, D. (2007). Statistical analyses and reproducible research. Journal of Computational and Graphical Statistics 16, 1–23](http://www.tandfonline.com/doi/abs/10.1198/106186007X178663#.VSMBK-7F89w)

[Gentleman, R. and Temple Lang, D. "Statistical Analyses and Reproducible Research" (May 2004). Bioconductor Project Working Papers.](http://biostats.bepress.com/bioconductor/paper2/)

Stodden, V and Miguez, S 2014. Best Practices for Computational Science: Software Infrastructure and Environments for Reproducible and Extensible Research. Journal of Open Research Software 2(1):e21, DOI: [http://dx.doi.org/10.5334/jors.ay](http://dx.doi.org/10.5334/jors.ay)

[Wickham, Hadley, R Packages: Organise, test, document, and share your code. O’Reilly.](http://r-pkgs.had.co.nz/)

### Colophon

This document was the result of discussions at the [2015 rOpenSci unconference](http://unconf.ropensci.org/) (cf. https://github.com/ropensci/unconf/issues/11 and https://github.com/ropensci/unconf/issues/31). Contributors to the discussion include... [if you were in the rOpenSci unconf breakout on this topic please add your name via a Pull Request]. This document was initially drafted by [Hadley Wickham](https://github.com/hadley), with later contributions from [Ben Marwick](https://github.com/benmarwick). Additional contributions are welcome! Please [post an issue](https://github.com/ropensci/rrrpkg/issues/) to ask questions and discuss suggestions.
