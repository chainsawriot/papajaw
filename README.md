# Motto

1. Reproduciblity: Thou shalt not copy and paste.
2. Single source of truth (FINAL.doc; FINAL\_rev2.doc; FINAL\_rev2\_commented.doc; FINAL\_correct\_reallyfinal.doc)
3. If this your first night, you have to type.

# Setup

## prerequisites

1. R installed (preferably on Linux / Mac OS X)
2. Google account (Optional, for Trackdown and RStudio Cloud instance)

```r
# setup Latex

install.packages(c("tinytex", "remotes", "trackdown"))
tinytex::install_tinytex()

## restart your environment, e.g. BASH
remotes::install_github("crsh/papaja")
```

You may also use the shared RStudio Cloud instance.

https://rstudio.cloud/project/4059380

# Create a new article

* RStudio

File -> New File -> R Markdown -> From Template -> APA Article (6th)

Editor-agnostic method

```r
rmarkdown::draft("article.Rmd", template = "apa6", create_dir = FALSE, package = "papaja", edit = FALSE)
```

# Immediate rendering

A good way to install missing LaTeX components.

```r
rmarkdown::render("article.Rmd")
```

# From here: FAQ

