
<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Travis-CI Build Status](https://travis-ci.org/CannaData/CannaBarcode.svg?branch=master)](https://travis-ci.org/CannaData/CannaBarcode)

shinyBarcode
============

The goal of `shinyBarcode` is to wrap the [JsBarcode](https://github.com/lindell/JsBarcode) library, written by Johan Lindell, for R. This enables rendering of barcodes in R Markdown and Shiny. This enables generating receipts in markdown, which can compiled to HTML with `rmarkdown`, and then printed using Google Cloud Print using [`googlePrintr`](https://github.com/CannaData/googlePrintr).

Installation
------------

You can install CannaBarcode from github with:

``` r
# install.packages("devtools")
devtools::install_github("CannaData/shinyBarcode")
```

Example
-------

### Shiny

``` r
library(shiny)
library(CannaBarcode)

ui <- fluidPage(
  # must include javascript dependencies
  CannaBarcode::includeJsBarcode(cdn = TRUE),
  numericInput("value", "Input a positive integer", 8675309, 0, 1000000),
  CannaBarcode::barcodeOutput("barcode")
)

server <- function(input, output, session) {
  output$barcode <- CannaBarcode::renderBarcode(
    input$value
  )
}

shinyApp(ui = ui, server = server)
```
