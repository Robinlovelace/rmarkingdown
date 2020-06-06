Robin Lovelace

# rmarkingdown

# Quickstart

To get started with this template:

  - Create a new RStudio project in a suitable place and with a suitable
    name, e.g. `~/modules/tds/marks-2020` and open it up.
  - Download and unzip the contents of this template with the following
    commands in the new project:

<!-- end list -->

``` r
u = "https://github.com/Robinlovelace/rmarkingdown/archive/master.zip"
download.file(u, "master.zip")
unzip("master.zip")
files_to_move = list.files(path = "rmarkingdown-master/", pattern = "*", full.names = TRUE)
destinations = basename(files_to_move)
file.copy(
  from = files_to_move,
  to = ".",
  overwrite = FALSE, # avoid deleting files
  recursive = TRUE
  )
```

# Introduction

This document contains code and text for evaluating and providing
feedback to students who submitted reports for the module
[xxx](web-link). It aims to use the power of RMarkdown (Allaire et al.
2018) to automate some parts of the process, and to provide individual
(for students), and whole assessment level reports (for staff) in
RMarkdown and html (or other) formats. The feedback is designed to be
constructive.

## Feedback criteria

Feedback is assessed using the following criteria, partly influenced by
a document from the [Oxford Learning
Institute](https://www.learning.ox.ac.uk/media/global/wwwadminoxacuk/localsites/oxfordlearninginstitute/documents/overview/rsv/Guidelines_for_giving_and_receiving_feedback.pdf),
under the following headings:

  - Demonstration of learning outcomes
  - Reproducibility
  - Positives
  - Areas for improvement
  - Ideas for further research

<!-- ## Learning outcomes -->

<!-- Note: these are example learning outcomes -->

<!-- Reference will be made to the following learning outcomes. -->

<!-- Knowledge: -->

<!--     understand the principles underlying base and grid graphics -->

<!--     understand how toolkits build on grid graphics are structured -->

<!--     understand the choices involved in the effective use of colours and glyphs -->

<!--     understand the motivations underlying the choices made in visualization in R programming -->

<!--     use this understanding in customising graphical outputs -->

<!-- Skills: -->

<!--     assign correct descriptions to visualization techniques used in scripts and functions encountered in simple workflows -->

<!--     define new visualization templates for workflow output -->

<!-- General competence: -->

<!--     handle the graphical output of R functions with greater confidence -->

<!--     customise the graphical output of R functions to meet specific needs -->

## Set-up

Template feedback files were created as follows:

``` r
# Adapt this for your own feedback:

feedback_template = "
# Candidate

## Positives

## Ideas for further research

## ...
"
```

You can also read-in a feedback template (recommended for modularity):

``` r
feedback_template = readLines("feedback-template.Rmd") # from known source

n_submissions = 3

submission_numbers = formatC(x = 1:n_submissions, width = 2, flag = 0)
lapply(submission_numbers, dir.create)
submission_names = paste0("submission", submission_numbers, ".Rmd")

# test writing template file
write_template = function(x) {
  writeLines(text = feedback_template, con = x)
}
write_template(submission_names[1])
rmarkdown::render("submission01.Rmd")
```

You can explore the template results before writing detailed feedback as
follows:

``` r
browseURL("submission01.html") # looks good
```

And create the template for all submissions like this:

``` r
# create all template files
purrr::map(submission_names, ~write_template(.))
```

# Feedback

After running the above code chunks mark each submission by editing each
.Rmd file, e.g. with:

``` r
file.edit("submission01.Rmd") # mark submission1
file.edit("submission02.Rmd") # mark submission2
file.edit("submission03.Rmd") # mark submission3
```

This can then be included with the following chunk setting:

    {r test-main1, child = 'submission01.Rmd'}

# Candidate

## Demonstration of learning outcomes

## Reproducibility

To reproduce the analysis, I tried to run the following commands:

## Positives

## Areas for improvement

## Ideas for further research

# submission 2: no submission

# Candidate

## Demonstration of learning outcomes

## Reproducibility

To reproduce the analysis, I tried to run the following commands:

## Positives

## Areas for improvement

## Ideas for further research

# Auto-generating submission chunks

Another step that can be automated is generating the Rmarkdown chunks
for each submission. This can be done as follows:

    make_chunk_submission = function(n) {
    
    paste0("
    
    
    
    ")
    }
    make_chunk_submission("01")
    
    make_chunk_submissions = function(submission_numbers) {
      purrr::map_chr(submission_numbers, make_chunk_submission)
    }
    
    chunk_submissions_text = make_chunk_submissions(submission_numbers)
    writeLines(chunk_submissions_text, "chunk_submissions_text.Rmd")
    file.edit("chunk_submissions_text.Rmd")

## References

<div id="refs" class="references hanging-indent">

<div id="ref-R-rmarkdown">

Allaire, JJ, Yihui Xie, Jonathan McPherson, Javier Luraschi, Kevin
Ushey, Aron Atkins, Hadley Wickham, Joe Cheng, and Winston Chang. 2018.
*Rmarkdown: Dynamic Documents for R*.

</div>

</div>
