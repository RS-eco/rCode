Write, structure and manage your code using RStudio & Git
================

## Rationale

We should always aim to make our work reproducible and easily
understandable by the reviewers and the target audience, as well as our
collaborators and co-authors. In addition, scientific journals nowadays
usually require that code and data is published online, for example in a
GitHub repository. You, but also other people, can benefit from this, as
everyone can easily access and re-use code from other people or past
publications, given that the code is understandable and structured in a
clear and reproducible way.

In addition, a well-structured and well-organised repository of your
code, including all the required dependencies, i.e. data files, will
make it a lot easier for you to revise your analysis, figures and
manuscript during the process of publication. Uploading these onto a
version-control repository, such as GitHub, will make it a lot easier to
track changes in your code, backup your work and collaborate/write code
together with your peers.

Over the last few years, I have come up with what I think is a “neat
way” to structure my code and my GitHub repositories, which I have
tried to outline here. Of course this strategy is subject to change, so
if you have any suggestions for improvement, if something is unclear or
if you still have questions regarding other unmentioned aspects, please
do not hesitate to contact me and I will include them in here.

## Setting-up your project

When you start with a new project/paper/PhD chapter, I would recommend
you to first create a new repository on GitHub and then set-up a new R
project from within RStudio, which is linked to the repository on
GitHub.

R projects have a very useful functionality, they automatically set your
working directory to the location of the project folder (which you
created, when you set-up a new project). So when you restart RStudio you
just have to re-open again the R project and you do not have to specify
your working directory in the beginning of your code. In addition, if
you are collaborating with other people or you are sharing your work
with your supervisor, this will make sure the code is also working on
his or her computer without having to change anything in the code (this
is what I call reproducible research/coding).

**A very important note:** To write reproducible code, never use your
working directory in filepaths (`list.files("/home/matt/Documents/")`)
but use relative paths (`list.files("/data")`). If you really have to
specify your working directory, do this only once and in the beginning
of your script, i.e. before or directly after you load your required
packages, i.e. `library(dplyr)`.

## Storing your project

Ideally, you use some sort of version control (GitHub) for your
projects, so you can track changes in your code without having to save
different versions of it, and additionally all your work is
automatically backed up. A version control software like GitHub is
fundamentally different to cloud storage facilities, such as Dropbox, as
you can go back to every stage of your work, i.e. see what your code
looked like 1 month, 6 months or 2 years ago. However, this also means
that a lot of data (all the past versions) are stored in the background,
which means that you should only upload small files, mostly code and
maybe small datasets. For this reason, GitHub for example limits the
individual file size to 50 MBs (see also the section on large data
files). I would recommend you to use GitHub, if you are not doing so
already. Make sure that you upgrade your account to an education
account, so that you have unlimited private repositories, which you only
make public once the R package is working or once your paper has been
accepted for publication. Of course, you can still share private
repositories with other users, i.e. your co-authors, but only those
people that you have added to the repository can access it. **Let me
know, in case you have problems, setting up private repositories, and I
can show you how to upgrade your account.**

If you are collaborating with other people and multiple people are
writing code at the same time, version control is the way to go. There
is no need to save different versions with your name highlighted, i.e.
“change\_projection\_MB.R”, as you can see through the version control
automatically, who has edited which line of code. **Note: Version
control softwares, like GitHub,** can save updated copies of any file
type, but **cannot track changes**, i.e. Max has changed line 5 of
“change\_projection.R”, **of some file types, i.e. Word documents**.
If you want to have a trackable version of your manuscript, I would
recommend to stop using Word and write your manuscript/text in RMarkdown
or Latex, then you are also able to track changes of manuscripts and
multiple people can edit the same document simultanousely.

A cool collaborative feature of GitHub, which is still hugely under-used
in our group, are issues. Issues can be used to track todos, bugs,
feature requests, and more. And I personally would suggest to use this
to communicate and distribute coding tasks among people and keeping
track of the current status of the work, rather than using other
softwares/platforms like Trello.

To keep things simple, RStudio has a Git interface included, which means
you can track your changes, submit new commits (changes), revert changes
and so on, all within RStudio. I find this the easiest way to work with
GitHub unless you are super keen on using the command line.

<!-- Also talk about branches!!! -->

## Structuring your project

I recommend to store code and all required/dependent data objects of
your code in a way, so that it is easily understandable also for other
non-familiar users, like your supervisor, but also in the most flexible
way possible. So rather than writing code and functions that only work
for one dataset, think of other people or other datasets, where you or
someone else might want to perform the same task. Ideally, this means
you would write your code in a way that you can use it for all
anticipated tasks right from the beginning, rather than spending a lot
of time adapting your 100 line code later on just to re-run the same
code with another dataset. Sometimes you might not anticipate using your
code with another dataset, i.e. when the reviewer of your paper says he
wants you to use occurrence data rather than range maps, then you might
also wish you would have written your code in a more flexible and easily
adjustable manner.

I would recommend you to structure each repository/project similar to
the general structure of an R package. If you are super interested, you
can find a more detailed information here:
<https://cran.r-project.org/doc/manuals/R-exts.html#Package-structure>
or you can ask me about how to write your own R package, but for now I
will explain everything you really need to know in the next paragraphs.

R packages typically have various subdirectories (R, data, extdata, …).
I would recommend you to arrange your code and files into those three
subdirectories (R, data and extdata). In addition, you might also want
to create a subdirectory “figures”, in which you can store all the
created figures.

The name of the subdirectories might not be very important, but
detrimental in case you might want to turn your code into an R package.
This might not be the overall goal for most of you, but might come in
handy, if you are going to base a study/PhD chapter on previous work,
which you could then easily access by calling the previous work/R
package with a simple `library("yourproject")` call.

To give you an example, for one of our projects, I created one repo for
processing IUCN and BirdLife range maps (“rasterSp”) and two repos for
processing the ISIMIP2b global climate data (“rISIMIP” & “processNC”).
These were very generic repos, which could be useful for other people or
different projects, so I have turned them into separate R packages,
which are available on GitHub (<https://github.com/RS-eco>) and can
easily be loaded and used in new projects using
`devtools::install_github()`.

## R-Scripts

Most of the time you will probably work on an R script, which reads your
data, performs different analyses, creates different figures, …

I would recommend to separate your scripts, so that each script serves a
certain purpose and is not too long. Also make sure that the script has
a name, which clearly states what the script does, so if someone who is
not familiar with your scripts knows where to find what they are looking
for.

Another recommendation, which has proven quite useful if you end up with
a lot of scripts, add a number to the beginning of the name of your
script, i.e. 01\_VariableCorrelation.R, and order the numbers of the
scripts according to a logical order (ideally the numbering of the
scripts represents a step-by-step analysis). For example, it would not
make much sense to perform a variable correlation after you have done
your models, so the variable correlation script should have a smaller
number than the modelling script (i.e. 01\_VariableCorrelation.R,
02\_RunModels.R).

### Structuring and writing scripts

The first thing all your scripts should include is a YAML header with at
least two specifications, the title and author(s) of your script. YAML
headers have a certain style, so R understands them, see for example
here: <https://bookdown.org/yihui/rmarkdown/html-document.html>.

The YAML header of an R-script, would typically look like this:

``` r
#' ---
#' title: "Create overview figures"
#' author: "RS-eco"
#' ---
```

**Note:** The author argument can also take multiple authors, but should
always say “author:” in the beginning, i.e. `author: "Max & Peter"`.

I would further recommend to write your R Scripts in a way, that they
can be compiled into a report (A nice feature that is also included in
RStudio) or if you are familiar with RMarkdown, you can also write your
R scripts as .Rmd files, although I have now moved away from RMarkdown
again and prefer the plain R Scripts, as people who are not familiar
with RMarkdown can then still make use of your code.

Regardless, whether you compile your scripts into a report or not, I
would suggest two small, but important things, when writing and saving
your scripts:

1.  All your scripts should be saved directly in the project folder, and
    **not inside a subfolder**. This makes sure, that if you want to
    create a report from your script, the file paths are correct.

2.  To write comments inside your script do not use `#` but `#'`, this
    makes sure your comments will be converted into normal text, when
    compiling your report.

### Creating reports from scripts

Compiling reports from R scripts is super easy, see for example a short
video tutorial here: <https://www.youtube.com/watch?v=4xwaH9CR2TY>. More
information on compiling reports from R scripts can also be found here:
<https://rmarkdown.rstudio.com/articles_report_from_r_script.html>.

This is where the YAML-Header comes in very useful, as during
compilation R automatically recognizes those fields as author and title,
rather than adding a default title and author value.

The good thing about creating reports is, that when you try to compile a
report from your script, it will execute your script sequentially and so
checks for you, if your script is actually reproducible or not. This
might be a little bit frustrating, if you are not good in writing clean
and reproducible code, but has the advantage, that it will help you to
improve your coding skills, but also to avoid problems later on when you
are trying to re-run your analysis or re-create certain results. \*\*To
overcome/avoid this problem, always write your code in a logical order,
i.e. do not jump back and forth in your script, do not overwrite objects
that you need later-on, and do not use objects that you have loaded from
a different R-script, every script should principially for itself,
excluding functions and stored data objects (see sections below).

Another advantage of compiling reports, is that you do not have to store
individual figures, but you can just store the report which includes all
created figures inside the script, and then directly show this to your
supervisor or co-authors. This has also the advantage that you don’t
have 1000 figures stored in one folder, which are hard to keep track of,
but that all your figures are automatically organised according to the
different steps of your analysis/scripts.

#### Chunk options

When you compile a report, all the R-code and its output will be
automatically included in the report. However, you can also change this
behaviour, by adding certain options in front of every R chunk. You can
do this by specifying certain chunk options, after writing `#+`, e.g.
`#+echo=FALSE`. Note that the `echo = FALSE` parameter prevents printing
of the R code.

There are five main chunk option arguments:

1.  `include = FALSE` prevents code and results from appearing in the
    finished file. R Markdown still runs the code in the chunk, and the
    results can be used by other chunks.
2.  `echo = FALSE` prevents code, but not the results from appearing in
    the finished file. This is a useful way to embed figures.
3.  `message = FALSE` prevents messages that are generated by code from
    appearing in the finished file.
4.  `warning = FALSE` prevents warnings that are generated by code from
    appearing in the finished.
5.  `fig.cap = "..."` adds a caption to graphical results.

In addition, you can also set a path for your output figures, with
`fig.path`, which I would recommend to set to `fig.path="figures`, in
case you want to store the figures as separate files in addition to the
report. This makes sure all figures are stored in a subfolder called
figures. And you can also specify the size of your figures, by using
`fig.width` and `fig.height`. If you specify a `fig.path`, you probably
also want to specify a chunk name for each figute, by giving your chunk
a label `#+ fig_var_cor, echo=F`, otherwise the figure names will be
created automatically and might not be very meaningful, if you are
looking for a certain figure later on.

See also the R Markdown Reference Guide
<https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf>
for a complete list of knitr chunk options.

**Please note:** If you compile reports from your scripts, i.e. word,
html or pdf files, do not commit them to your repository, as this is
kind of a redundant information to the R script and you and your
co-authors should easily be able to re-create them by simple
re-running/re-compiling your script.

### Writing scripts/code for multiple variables

A lot of people, which are not very familiar with good coding practices,
copy and paste there code multiple times to re-run the same code for
multiple features, i.e. to do the same analysis for different taxa
(amphibians, birds, mammals).

Even if you do not want to re-run the same code for multiple features, I
would recommend to specify all your dependent variables in the beginning
of your script (The same holds true for writing functions, see section
below). For example, let’s say we want to do an analysis for a certain
country (Germany), for a specific taxa (birds) and we want to look at a
certain environmental variable (tmean) and a certain time frame (1990 -
2000). Then the beginning of your script, should principally look like
this:

``` r
country <- "DEU"
taxa <- "birds"
var <- "tmean"
year <- ("1990-2000")
```

Of course, you might not need all of these variables straight from the
beginning, but the year or the environmental variable might just show up
in line 100, and/or you might only include some of them after writing
the code for several months. Nevertheless, you should always mention
those variables in the beginning of your script, as it makes it very
easy and fast to change one of those parameters later on.

This will also have consequences for the rest of your script, for
example if you are going to save a figure, you should add all these
variables to your figure name, in a way that your figure name is going
to change if you change the value of one of these objects, this could
for example look like: `ggsave(paste0("figures/", country, "_", taxa,
"_", var, "_", year, "sr_hist.png"))`.

As a consequence, I recommend to not name any objects according to the
value of any of these variables, for example do not call an object
`bird_richness`, but rather name the object `taxon-richness`. And the
name/title of the script should also not be called according to the
variable-specific values, i.e. “Temperature change of birds in Germany”,
but rather “taxon and country-specific changes in environmental
conditions”.

Ideally, if you then want to run the same analysis for another country
or taxon, all you have to do is change the relevant lines in the
beginning of your script, compile a new report and save a copy of the
report with a unique name, this time for example with the variable
values, i.e. “Bird\_tmean\_changes\_Germany.pdf”.

Of course, this would mean a lot of work in case you want to do this
analysis for 20 different countries. Then it will be more feasible to
include the whole code into a `for` loop or an `lapply` call to loop
through the same code over and over again. Or if you want to repeat a
short code chunk multiple times with different variables, it might be
even easier and more efficient to write functions for this (see next
section).

**Side note:** If you are running a loop to create multiple versions of
the same Figure, i.e. one figure for every species, it can be helpful to
store all figures into one PDF file with multiple pages (one for every
species). This can be easily done by running a loop inside a plotting
command and would look something like this:

``` r
pdf("figures/species-specific_rangemaps.pdf")
for(i in 1:length(species)){
  plot(dat[dat$species==i,])
}
dev.off()
```

## Functions

### Using functions

Code or code chunks that you are going to use multiple times are best
stored in functions, for example a certain plotting theme:

``` r
theme_map <- function(base_size = 10, base_family = "") {
  theme_classic(base_size = base_size, base_family = base_family) %+replace%
    theme(axis.line = element_blank(), axis.ticks = element_blank(),
          axis.text = element_blank(), axis.title = element_blank(), 
          panel.border = element_blank(), 
          plot.title = element_text(size = base_size, face = "bold", hjust = 0.5))
}
```

You can even use functions to read in your pre-processed dataset or
database or create a function for an entire plot/map.

**Note:** Your functions should always be written in a way, that they
can be used universally, or at least as universally as possible, and do
not just solve/fit for one purpose/one dataset. To achieve this, all
objects that are used/needed by the function should be included in the
function argument, as otherwise you might not be able to use the
function if any of the included objects has changed, or you or someone
else will have a hard time getting your function to work if one of the
dependencies has changed. **If you do not specify all required objects
as an argument, there is absolutely no point in using functions. **

Below, I will demonstrate what I mean with this, by giving several
examples (bad, good, perfect):

#### Bad example

``` r
df_transform <- function(coords=c("x","y"), crs.out=NA){
  if(class(data) == "data.frame"){
    data <- raster::rasterFromXYZ(data)
    raster::projection(data) <- sp::CRS("+init=epsg:4326")
    data <- raster::projectRaster(data, crs=crs.out)
    data <- as.data.frame(raster::rasterToPoints(data))
  } else{
    warning("Data has to be of class data.frame.")
  }
  return(data)
}
```

The above code is an example of how not to write a function, as it
assumes that you have already loaded a dataset called “data”. To solve
this, you would just have to include “data” to the function arguments.
In addition, the function sets the projection to a certain input
projection, which could change depending on the input dataset you used,
so ideally you would also include a function argument, i.e. crs.in, so
the function can be used with any dataset and any input projection.

#### Good example

``` r
df_transform <- function(data, coords=c("x","y"), 
                         crs.in=sp::CRS("+init=epsg:4326"), crs.out=NA){
  if(class(data) == "data.frame"){
    data <- raster::rasterFromXYZ(data)
    raster::projection(data) <- sp::CRS("+init=epsg:4326")
    data <- raster::projectRaster(data, crs=crs.out)
    data <- as.data.frame(raster::rasterToPoints(data))
  } else{
    warning("Data has to be of class data.frame.")
  }
  return(data)
}
```

This example is a bit better, as it includes the data argument in the
function. It also specifies the input projection (crs.in) and even sets
the crs.in to a default value, i.e. the most commonly encountered
projection in spatial data (WGS84/LonLat). crs.out does not have a
default value, as this will be case specific and I do not know which
output projection the user might want. However, the example stil lacks a
documentation of the function and also does not give a universally
applicable example, which you could/should use to test if your function
can be applied universally. I have demonstrated how this is usually
done, when writing functions inside an R package, in the example below:

#### Perfect example

``` r
#' Transform projection of data.frame
#'
#' @description Change the projection of x and y values (spatial coordinates) 
#'              of a data.frame, make sure your data only includes x,y and z 
#'              and no additional categorical variables
#' 
#' @usage 
#' df_transform(data, coords, crs.in, crs.out)
#' 
#' @param data data.frame object
#' @param coords vector of the two coordinate column names
#' @param crs.in original projection of data.frame, standard is WGS1984.
#' @param crs.out output projection of data.frame, which is returned.
#' @details df_transform internally converts the data.frame into a spatial object, 
#' than transforms the projection of the data and 
#' converts the final spatial object back into a data.frme.
#' @return A data.frame
#'  
#' @examples
#' data(meuse, package="sp")
#' meuse <- df_transform(meuse, 
#'                       crs.in=sp::CRS("+init=epsg:28992"), 
#'                       crs.out=sp::CRS("+init=epsg:4326"))
#'
#' @export
df_transform <- function(data, coords=c("x","y"), 
                         crs.in=sp::CRS("+init=epsg:4326"), 
                         crs.out=NA){
  if(class(data) == "data.frame"){
    data <- raster::rasterFromXYZ(data)
    raster::projection(data) <- crs.in
    data <- raster::projectRaster(data, crs=crs.out)
    data <- as.data.frame(raster::rasterToPoints(data))
  } else{
    warning("Data has to be of class data.frame.")
  }
  return(data)
}
```

<!-- Add note on how to use package functions (raster::) inside functions. -->

### Writing and reading functions

You should store your written function, for example the code and
description of the “perfect” example, in an R file, which usually has
the same name as the function itself, i.e. “df\_transform.R”. Usually
every function is stored in a separate file, but sometimes, if multiple
functions serve similar purporses or depend on each other, it also makes
sense to combine multiple functions into one file. Those functions are
commonly saved in a subfolder called “R”. If you want to load your
stored functions, you just have to use `source()`, i.e.
`source("R/df_transform.R")`.

## Data files

### When to create files

Generally, I would recommend to save as little output files as possible.
Of course, you can run three lines of code and save the output and end
up with a 100 different data files in a short time, but I would
recommend to only do this, if individual tasks take a long time (more
than 1-2 min) to run. The output of code that only takes a few seconds
to run, does not need to be saved in a single file, as this file might
be subject to change and could potentially mess up your results if you
forget to re-run all code that depends on this file.

If you create files, because you want to look at them in Excel, you can
of course always save your output, even something that can easily be
re-run, but then do not build any analyses on this file, but on the code
to create the file and do not store this file on GitHub.

### Storing data

Small data files, that are detrimental for your analysis, should be
stored in a subfolder called “data”. You can then easily read those
files, for example with `read.csv("data/yourfile.csv")`.

Another useful tipp from my side, think about all the possible files you
are going to create in advance and how they might be named. If we go
back to the last example, we would have files for different countries,
taxa, years and variables, so you should make sure that all of these
specifications end up in your file naming, something that is generally
specified by a certain file naming convention, which could actually
state in the beginning of your script or somewhere where people can read
it, so they can easily get an overview of all the different output files
or figures you have created.

Last but not least, you should also think about the structure of the
data and the best and most versatile way to store those data. You should
ask yourself the following questions and depending on the answer should
decide on the best structure and format of your data.

1.  Does it make more sense to store data in a wide or a long-table
    format?
2.  Which columns of my data do I really need and which are already
    stored somewhere else?
3.  How often do I need to access this data? If you need to read in the
    data quite often, you want a file that you can read quickly, while
    if you need the data not that often but it is quite large, you might
    want to store the file in a way that it takes up the least space.

For our last project, I had to change all of our final output files into
a different format to publish our data in accordance with other people’s
data. As we created several TBs of data, changing the format of this
data took quite a long time. Something, I could have avoided if we would
have organised our code in a way, so that we would have stored our
output directly in the best way, from the beginning.

### Large data files

As I have mentioned before GitHub only allows you to upload files
smaller than 50 MBs. R becomes really slow when reading in large
datasets (but see note at the bottom of this section), so I would anyway
recommend you to not store any data in files larger than 50 MBs.
However, sometimes this cannot be avoided. I would recommend to story
preliminary files, files that are too large or files that are not
necessarily required in your analysis into a subfolder called
(“extdata”), which stands for external data. However, make sure that
you do not add/commit those files to your GitHub repository. You can
also add these file to the .gitignore file inside your project folder,
then GitHub automatically ignores those files.

Although, there are some possibilities to include large files on GitHub,
see Git Large File Storage (<https://git-lfs.github.com/>), I would try
to avoid it, as storing lots of data in the cloud creates quite a large
environmental footprint, something you should also always consider
before storing unnecessary and duplicated information on your GitHub
repository or in the cloud.

Large files are usually not going to change that often anyways, so if
you are collaborating with multiple people, I would suggest to
distribute those large files, i.e. for example databases, by other means
(LRZ Sync+Share, wetransfer.com or the old fashioned way by memory stick
or hard drive) and ask those people to copy those files into the
“extdata” folder in the project folder. Than you can all read those
large files, by calling for examples
`read.csv("extdata/yourlargefile.csv")`, and your code is still
reproducible as long as people have access to the file and have loaded
it into the correct folder. **Note:** This is also the preferred way if
you are dealing with sensitive data, which you should not store online
or make accessible to other people.

If you are reading in external files that you need for multiple
projects, for example WorldClim data, of course it would not make much
sense to always copy those data into every project folder, as this will
fill up the memory of your hard drive quite quickly. For this case, I
would recommend to create a “Data” folder outside your individual
projects, which you can then link to by specifying a file directory
(filedir) variable in the beginning of your script:

``` r
filedir <- "/home/matt/Documents/Data"
```

When ever you read in a file from this folder, which can of course have
multiple subfolders, you always provide a path that links to the
“filedir” and not the full path, for example:

``` r
worldclim <- read.csv(paste0(filedir, "/Worldclim/yourfile.csv"))
```

That way, every person see right away when they open your script, that
they have to specify a file directory path and once they have set that,
your code is again still reproducible, without having to change anything
else.´

**An additional off-topic note:** If you want to work/access large
datasets (\> 10 GB) in R you will often struggle to access them and/or
your computer will be super slow, as R reads all this data into memory.
There are multiple ways of dealing with this, there are also new
packages in development, but one of the best ways around it is to turn
your data into a database. If you ever need help with this, I can send
you an explanation/guideline of how to do this just using R.
