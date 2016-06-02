# Fetch File
Bill Kerneckel, Kyle Killion, Eyal Greenberg  
May 28, 2016  

## Fetch file instructions to download the orginal2011 Brooklyn real estate data

<br>

#### Step 1 - Download the data
The data comes from the offical website of the City of New York located at <a href="http://www1.nyc.gov/">www.1.nyc.gov</a>. You can download the orginal data set at <a href="http:http://www1.nyc.gov/assets/finance/downloads/pdf/rolling_sales/annualized-sales/2011/2011_brooklyn.xls">[XLS] Brooklyn Data</a>. Once you have downloaded the data place the file into your working directory.
<br>

<br>

#### Step 2 - Load the data
`````````````
require(gdata)

require(plyr)

Important! Make sure you set your working directory to the location you saved the downlaoded to.
setwd("/Users/*Username*/documents")

Note: If you plan on using the .XLS format use this command line
bk <- read.xls("2011_brooklyn.xls",pattern="BOROUGH")

Note: If you plan on using the .CVS format use this command line
bk <- read.cvs("2011_brooklyn.cvs",skip=4,header=TRUE)

`````````````

<br>



