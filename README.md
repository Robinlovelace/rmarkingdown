Robin Lovelace

# rmarkingdown

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
  - Ideas for further
research

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

## Demonstration of learning outcomes

## Reproducibility

## Positives

## Areas for improvement

## Ideas for further research
"
feedback_template = readLines("feedback-template.Rmd") # from known source

n_groups = 3

group_numbers = formatC(x = 1:n_groups, width = 2, flag = 0)
lapply(group_numbers, dir.create)
group_names = paste0("group", group_numbers, ".Rmd")

# test writing template file
write_template = function(x) {
  writeLines(text = feedback_template, con = x)
}
write_template(group_names[1])
rmarkdown::render("group01.Rmd")
```

You can explore the template results before writing detailed feedback as
follows:

``` r
browseURL("group01.html") # looks good
```

And create the template for all groups like this:

``` r
# create all template files
purrr::map(group_names, ~write_template(.))
```

# Feedback

After running the above code chunks mark each group by editing each .Rmd
file, e.g. with:

``` r
file.edit("group01.Rmd") # mark group1
file.edit("group02.Rmd") # mark group2
file.edit("group03.Rmd") # mark group3
```

This can then be included with the following chunk setting:

    {r test-main1, child = 'group01.Rmd'}

# Candidate 1

This content was written manually. Note you can still include references
(Lovelace, Nowosad, and Muenchow 2019).

## Demonstration of learning outcomes

## Reproducibility

To reproduce the analysis, I tried to run the following commands:

## Positives

## Areas for improvement

## Ideas for further research

# Group 2: no submission

# Candidate

## Demonstration of learning outcomes

## Reproducibility

To reproduce the analysis, I tried to run the following commands:

## Positives

## Areas for improvement

## Ideas for further research

# Auto-generating group chunks

Another step that can be automated is generating the Rmarkdown chunks
for each group. This can be done as follows:

    make_chunk_group = function(n) {
    
    paste0("
    
    
    
    ")
    }
    make_chunk_group("01")
    
    make_chunk_groups = function(group_numbers) {
      purrr::map_chr(group_numbers, make_chunk_group)
    }
    
    chunk_groups_text = make_chunk_groups(group_numbers)
    writeLines(chunk_groups_text, "chunk_groups_text.Rmd")
    file.edit("chunk_groups_text.Rmd")

## References

<div id="refs" class="references">

<div id="ref-R-rmarkdown">

Allaire, JJ, Yihui Xie, Jonathan McPherson, Javier Luraschi, Kevin
Ushey, Aron Atkins, Hadley Wickham, Joe Cheng, and Winston Chang. 2018.
*Rmarkdown: Dynamic Documents for R*.

</div>

<div id="ref-lovelace_geocomputation_2019">

Lovelace, Robin, Jakub Nowosad, and Jannes Muenchow. 2019.
*Geocomputation with R*. CRC Press.

</div>

</div>
