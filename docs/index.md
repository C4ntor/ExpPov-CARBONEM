# EXPPOV PROJECT

## Linking HBS with EXIOBASE


### Mathematical Background and Notation
We will extend the notation used by [pymrio documentation](https://pymrio.readthedocs.io/en/latest/math.html) 

Recall \(Y\) to be Demand Matrix of size \(9800 \times 9800\)

The linking process involves several steps:

0) solve leontief model (find \(X\)),S matrix must be divided by 1000000 in order to get 1 euro (unit) effect , fix an environmental factor \(S_i\) and compute:   

Following pymrio we compute \(X=L \cdot Y_a\) to get the total footprints. Where \(Y_a\) is a matrix of size \(9800 \times 49\) where each column is the total demand vector for respective region given by the aggregation of all 7 demand categories for the region in original demand matrix Y. 
An alternative approach would be to compute \(X=L \cdot Y_c\) where \(Y_c\) is matrix \(9800 \times 49 \) where each column now only contains the household consumption demand from Y.

The desired output will be a matrix of size \(9800 \times 49\), where i-th column  represents footprint table of each exiobase category for the i-th region (indeed it is given as demand of region i from \(Y_a\) multiplied for corresponding categories env factor).  
(like considering transpose of S_i as convolution filter, no summing, over the column of X) 
in order to get it, an element wise multiplication between \(S_i\) and X must be performed. A new X matrix, containing now env requirements for each region aggregated demand (col)  is obtained.

1) for each column of \(X\), say \(X_i\),  we produce the hbs categories - region specific - footprints as follows:
Consider both [COICOP_EU_ini.xlsx and COICOP_EXIOBASE.xlsx files](https://ntnu.app.box.com/v/EXIOBASEconcordances/folder/47855342420) from Richard Wood NTNU, Since the HBS is partially based on the COICOP we proceed as follows:
We replace Coicop labels from COICOP_EU_ini.xlsx with COICOP Codes that can be found in COICOP to EXIOBASEprod table of the latter file.
Furthermore it is possible to notice that each COICOP Codes has a correspondence with HBS EUR_HE Category as follows: remove  any occurence of 'c' and '.' from coicop code, pre-append 'EUR_HE' to get HBS Category. 

Recall that EUR_HExx are home-consumptions and EUR_HJxx are consumptions done abroad.
2) Each EUR_HExx category (say at position/row i for weight_map) is determined as sum dot product between weight_map[i] and \(reg_X_i\), where \(reg_X_i\) is filtered \(X_i\) where region=Current region for which we are computing the footprints. One could also exclude the export demand category when computing EUR_HExx.
Each EUR_HJxx category is determined as aggregation of 
 







## Installation

Place exiobase-coicop-hbs conversion tables (COICOP_EU_ini and COICOP_EXIOBASE) into the weight_map folder,
Place HBS-country-year files into the working_DIR/year path
   


## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

# Documentation

## Test
::: src.main

