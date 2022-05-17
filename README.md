# Motto

1. Reproduciblity: Thou shalt not copy and paste.
2. Single source of truth in a Git repository (not FINAL.doc; FINAL\_rev2.doc; FINAL\_rev2\_commented.doc; FINAL\_correct\_reallyfinal.doc)
3. If this is your first night, you have to type.

# Setup

## prerequisites

1. R installed (preferably on Linux / Mac OS X)
2. Google account (Optional, for Trackdown and RStudio Cloud instance)

```r
# setup Latex

install.packages(c("tinytex", "remotes", "trackdown", "here", "broom"))
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

# here

Announcing this is the base directory (Please don't `setwd`)

```r
here::i_am("article.Rmd")
```

# From here: FAQ

**Q: I need Microsoft Word.**

A: Change `output` to `papaja::apa6_word`

**Q: This is for anonymous peer review**

A: Change `mask` to `yes`

**Q: I need to insert a table**

A: Change your table to a data frame and use `apa_table`

For example:

```r
media <- read.csv(here::here("data", "media.csv"))

model <- lm(radio~gender+age+education, data = media)
broom::tidy(model, conf.int = TRUE)

papaja::apa_table(broom::tidy(model, conf.int = TRUE))
```

Or add this into your rmarkdown as a code chunk

```markdown
```{r, echo = FALSE}
media <- read.csv(here::here("data", "media.csv"))
model <- lm(radio~gender+age+education, data = media)
papaja::apa_table(broom::tidy(model, conf.int = TRUE), caption = "Very important regression table", note = "You need to read this")
```

**Q: I need to insert a figure**

A: You have the figure file.

```r
knitr::include_graphics(here::here("fig", "survivorship.png"))
```

You want to generate the figure on the fly.

```r
require(ggplot2)
ggplot(media, aes(x = radio, y = age)) + geom_point()
```

**Q: I want the figures and tables not at the back.**

A: Change `floatsintext` to `yes`

**Q: I want to cite something.**

A: You need to have your own Bibtex file (You can manage your bib file using Zotero, but that's beyond the scope of this short tutorial.)

1. Create a empty text file, e.g. "bib.bib"

2. Add entries

* Paste from downloaded bibtex files
* Generate from Crossref
* Google Scholar

3. Add to yaml `bibliography`

```markdown
@Van_der_Pas_2020 has said something great. This article [@Nanz_2022] says what I want to say. These articles [@Van_der_Pas_2020; @Nanz_2022] are nice.
```

**Q: I want to create a reproducible workflow.**

A: My suggestion is actually using [make](https://monashbioinformaticsplatform.github.io/2017-11-16-open-science-training/topics/automation.html).

**Q: I want to ...**

A: You probably can find out how to do that either in

* [The official papaja manual](http://frederikaust.com/papaja_man/)
* [The RMarkdown book](https://bookdown.org/yihui/rmarkdown/)

Or zillion of RMarkdown tutorials (e.g. this [one](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3175518) by my colleague Paul Bauer) out there. 
