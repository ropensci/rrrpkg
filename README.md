# rrrpkg
Use of an R package to facilitate reproducible research

## Research compendia

The goal of a research compendia is to provide a standard way for organising an reproducible research project with R, particularly those that result in the publication of a paper.

A research compendia is a convention for how you organise your research artefacts into directories:

Reusable functions go in the R/ directory.
Raw data lives in the data/ directory.
Analysis scripts and reports go in the analysis/ directory. An optional DESCRIPTION file describes the software dependencies of the compendia.
A README.md describes the overall project and where to get started.

The goal is to make a make convention that many people use. The convention helps people instantly familiarise themselves with the structure of a new project, and also supports tool building which takes advantage of the shared structure.

If you’re familiar with R packages, you’ll notice many similarities with these conventions. But there are some differences:

Stand alone vignettes tend not to be a great way to organise complex computation because they don’t make the ordering explicitly (or give the big picture).
Documentation and testing tend to be less important for compendia than packages - they are still important, but they tend come later in the process, and are used by relatively more advanced/experienced compendia users. 

Best way to share is to use github, but putting on dropbox.

R/

Focus of the code is reusable functions. This is often a small part of an analysis but it’s important.

data/

May be worthwhile to include small sample dataset that so that people can try out the techniques without having to run very expensive computations

analysis/

The analysis/ directory should include either a Makefile or a Makefile.R that controls the order of the code.
In many cases it will be useful to give the analysis scripts ascending names, e.g. 1-load.R, 2-clean.R etc (but this only gives a linear ordering, it doesn’t capture the full tree of dependencies)


DESCRIPTION

README.md

Useful to include graphical summary of the interlocking pieces of the project.

### Getting to that point
“Each analysis is perfect the way it is — and it can use a little improvement”.

Start simple - it’s ok to have just one R script or one R markdown file. But as you get more complex and start to break into multiple files, that you should follow these simple conventions.
Need to have a suggested plan of priorities: start here, then do x first, then y, then z.
Is it possible to take an RMarkdown document and “compile” it into this style of  compendia?

### Work needed

Make is a bottleneck for new users - having to learn 2 new languages at the same time is exponentially harder than just using one.
Need a package like devtools that automates the common problems and includes
Try out with a research project with this structure and report back in one year.
Would be useful to share these processes in public so that people have can good examples that they can look at

### Related research

http://biostats.bepress.com/bioconductor/paper2/
Op`en science framework
