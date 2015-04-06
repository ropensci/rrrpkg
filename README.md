# rrrpkg
Use of an R package to facilitate reproducible research

### What is a research compendium?

>We introduce the concept of a compendium as both a container for the different elements that make up the document and its computations (i.e. text, code, data,...), and as a means for distributing, managing and updating the collection. - Gentleman, R. and Temple Lang, D. (2004)

The goal of a research compendium is to provide a standard and easily recognisable way for organising an reproducible research project with R. A research compendium is ideal for projects that result in the publication of a paper because then readers of the paper can access the code and data that generated the results in the paper. A research compendium is a convention for how you organise your research artefacts into directories. The guiding principle in creating a research compendium is to organise your files following conventions that many people use. Following these conventions with help other people instantly familiarise themselves with the structure of your project, and also supports tool building which takes advantage of the shared structure.

### Why create a research compendium?

Using research compendia simplifies file management and streamlines analytical workflows, making your research more efficient. A compendium makes it easier to communicate your work with other researchers (and your future self), to demonstrate the correctness of your results. This can lead to higher visibility of your work, receiving credit for code as well as the paper, a boost in citations, and allows others to more easily build on your work. 

### How to make a research compendium

 At its simplest, a research compendium might consist of a single file of R code with inline comments documenting the workflow. A slightly more complex approach might be a R markdown file with text and code in the same source document. In many cases these simple approaches will be ideal, and more elaborate organisation would add unnecessary complexity and points of failure. But many projects will require some additional organisation to make them easier to work with. An ideal organisation for a more complex project would look like this:

* A **README.md** file that describes the overall project and where to get started. It's helpful to include graphical summary of the interlocking pieces of the project.
* Script files with reusable **functions** go in the `R/` directory. This is often a small part of an analysis but it’s important.
* Raw **data** files live in the `data/` directory. If your data are very large, it may be worthwhile to include small sample dataset that so that people can try out the techniques without having to run very expensive computations
* Analysis **scripts and reports** files go in the `analysis/` directory. The `analysis/` directory should include either a makefile or a makefile.R that controls the order of the code. In many cases it will be useful to give the analysis scripts ascending names, e.g. 001-load.R, 002-clean.R etc (but this only gives a linear ordering, it doesn't capture the full tree of dependencies)
* An optional DESCRIPTION file describes the software dependencies of the compendia.

If you’re familiar with R packages, you’ll notice many similarities with these conventions. But there are some differences:

* Stand alone package vignettes are often used as the manuscript file, but may not to the best way to organise complex computation because they don’t make the ordering explicit (or give the big picture). A separate `analysis/` or `manuscript/` directory may be more helpful here, and many people use a makefile to organise file dependencies
* Documentation and testing tend to be less important for compendia than packages - they are still important, but they tend come later in the process, and are used by relatively more advanced/experienced compendia users. 

More complex research compendia include other package elements such as a licence, tests, continuous integration, and dependencies external to R, such as a dockerfile to replicate the computational environment that the analyses were originally conducted in. 

### How to share a research compendium

You should prepare your compendium using a version control system such as git. Then when you are ready to share it, the best way is to archive a specific commit of your compendium at a repository that issues permanent URLs such as [figshare](http://figshare.com/) or [zenodo](https://zenodo.org/) which give DOIs for archived files. Then you can circulate the version of your compendium that is the version that generated the published results. This means you have a publicly available snapshot of the code that matches the paper. Code development can continue after the paper is published, but with a DOI that links to a specific commit, other users of the code can be confident that they have the version that matches the paper. A DOI also simplifies citation of the compendium, so you can cite it in your paper (and others can cite it in their work) using a permanent URL. 

Putting your compendium on dropbox or google drive is another way to make the compendium easily available. 

### Getting started with a research compendium

* “Each analysis is perfect the way it is — and it can use a little improvement”.
* Start simple - it’s ok to have just one R script or one R markdown file. But as you get more complex and start to break into multiple files, that you should follow these simple conventions described above
* If you start with a single R markdown document and want to develop it into a package, see the [rlp](https://github.com/yihui/rlp) package, which has functions for this purpose. 
* Need to have a suggested plan of priorities: start here, then do x first, then y, then z.

### Challenges for future work

* Make is a bottleneck for new users - having to learn two new languages at the same time is exponentially harder than just using one. One solution to this is the  [remake](https://github.com/richfitz/remake) package, which allows you to write makefile-like files entirely within R.
* We could do with a package like devtools that automates the common problems and handles typical research workflow issues
* We all need to try out the R package structure with our actual research projects and report back in one year so see what works, what doesn't, and where the pain points are. 
* Would be useful to share these processes in public so that people have can good examples that they can look at

### Related projects 

- Several people already using R packages as research compedia have released template packages for others to use:  [Jeff Hollister's manuscriptPackage](https://github.com/jhollist/manuscriptPackage), [Carl Boettiger's template](https://github.com/cboettig/template), and [Francisco Rodriguez-Sanchez's template](https://github.com/Pakillo/template). These are packages that give templates for organising an analysis as an R package (eg. where the manuscript is the package vignette, or similarly bundled with the package) 
-   For writing papers in R markdown, useful packages include include [captioner](https://github.com/adletaw/captioner) and [kfigr](https://github.com/mkoohafkan/kfigr) for figure and table captions and cross-referencing. 
-   For capturing the computational environment of an analysis, [rocker](https://github.com/rocker-org/rocker) is a project that provides Docker containers to run R in a lightweight virtual environment. The hadleyverse container includes dplyr, ggplot2, etc., as well as RStudio server and LaTeX. The package [harbor](https://github.com/wch/harbor) provides functions for controlling docker containers on local and remote hosts. The [analogsea](https://github.com/sckott/analogsea) package has functions for deploying R and RStudio quickly & easily on DigitalOcean clusters using Docker images for cloud computing. The [dockertest](https://github.com/richfitz/dockertest) package contains functions for generating Dockerfiles from R packages and other R projects, and building Docker containers that contains all the package dependencies.

### Further reading

[rOpenSci Guide to Reproducible Research](http://ropensci.github.io/reproducibility-guide/sections/introduction/)

[Gandrud C 2013 Reproducible Research with R and RStudio. CRC Press Florida](http://christophergandrud.github.io/RepResR-RStudio/)

[Gentleman, R. and Temple Lang, D. (2007). Statistical analyses and reproducible research. Journal of Computational and Graphical Statistics 16, 1–23](http://www.tandfonline.com/doi/abs/10.1198/106186007X178663#.VSMBK-7F89w)

[Gentleman, R. and Temple Lang, D. "Statistical Analyses and Reproducible Research" (May 2004). Bioconductor Project Working Papers.](http://biostats.bepress.com/bioconductor/paper2/)

Stodden, V and Miguez, S 2014. Best Practices for Computational Science: Software Infrastructure and Environments for Reproducible and Extensible Research. Journal of Open Research Software 2(1):e21, DOI: [http://dx.doi.org/10.5334/jors.ay](http://dx.doi.org/10.5334/jors.ay)
