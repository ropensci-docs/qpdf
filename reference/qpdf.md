# Split, Combine and Compress PDF Files

Content-preserving transformations transformations of PDF files. Note
qpdf does not read actual content from PDF files: to extract text and
data you need the pdftools package.

## Usage

``` r
pdf_split(input, output = NULL, password = "")

pdf_length(input, password = "")

pdf_subset(input, pages = 1, output = NULL, password = "")

pdf_combine(input, output = NULL, password = "")

pdf_compress(input, output = NULL, linearize = FALSE, password = "")

pdf_overlay_stamp(input, stamp, output = NULL, password = "", pages)

pdf_rotate_pages(
  input,
  pages,
  angle = 90,
  relative = FALSE,
  output = NULL,
  password = ""
)
```

## Arguments

- input:

  path or url to the input pdf file

- output:

  base path of the output file(s)

- password:

  string with password to open pdf file

- pages:

  a vector with page numbers to rotate/select/stamp depending on the
  function; for `pdf_select` negative numbers means removing those pages
  (same as R indexing)

- linearize:

  enable pdf linearization (streamable pdf)

- stamp:

  pdf file of which the first page is overlayed into each page of input

- angle:

  rotation angle in degrees (positive = clockwise)

- relative:

  if `TRUE`, pages are rotated relative to their current orientation. If
  `FALSE`, rotation is absolute (0 = portrait, 90 = landscape, rotated
  90 degrees clockwise from portrait)

## Details

Currently the package provides the following wrappers:

- pdf_length: show the number of pages in a pdf

- pdf_split: split a single pdf into separate files, one for each page

- pdf_subset: create a new pdf with a subset of the input pages

- pdf_combine: join several pdf files into one

- pdf_compress: compress or linearize a pdf file

- pdf_rotate_pages: rotate selected pages

These functions do not modify the `input` file: they create new output
file(s) and return the path(s) to these newly created files.

## Examples

``` r
# \donttest{
# extract some pages
pdf_file <- file.path(tempdir(), "output.pdf")
pdf_subset('https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf',
  pages = 1:3, output = pdf_file)
#> [1] "/tmp/RtmpBZEWMQ/output.pdf"
pdf_length(pdf_file)
#> [1] 3
unlink(pdf_file)
# }
```
