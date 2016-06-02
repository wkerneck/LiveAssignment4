# Clean File
Bill Kerneckel, Kyle Killion, Eyal Greenberg  
May 28, 2016  

## Clean file for 2011 Brooklyn real estate data
<br>



#### Step 1 - Perform some basic analysis on the data before we start tidying the data


```r
head(bk)
```

```
##   BOROUGH              NEIGHBORHOOD
## 1       3 BATH BEACH               
## 2       3 BATH BEACH               
## 3       3 BATH BEACH               
## 4       3 BATH BEACH               
## 5       3 BATH BEACH               
## 6       3 BATH BEACH               
##                        BUILDING.CLASS.CATEGORY TAX.CLASS.AT.PRESENT BLOCK
## 1 01  ONE FAMILY HOMES                                            1  6373
## 2 01  ONE FAMILY HOMES                                            1  6380
## 3 01  ONE FAMILY HOMES                                            1  6399
## 4 01  ONE FAMILY HOMES                                            1  6399
## 5 01  ONE FAMILY HOMES                                            1  6408
## 6 01  ONE FAMILY HOMES                                            1  6412
##   LOT EASE.MENT BUILDING.CLASS.AT.PRESENT
## 1  88        NA                        A1
## 2  71        NA                        A5
## 3   4        NA                        S1
## 4   7        NA                        S1
## 5  48        NA                        S1
## 6  31        NA                        A1
##                                     ADDRESS APARTMENT.NUMBER ZIP.CODE
## 1 92 BAY 23RD STREET                                            11214
## 2 8668 BAY PARKWAY                                              11214
## 3 1665 BATH AVENUE                                              11214
## 4 1657 BATH AVENUE                                              11214
## 5 1967 BATH AVENUE                                              11214
## 6 8701 21ST AVENUE                                              11214
##   RESIDENTIAL.UNITS COMMERCIAL.UNITS TOTAL.UNITS LAND.SQUARE.FEET
## 1                 1                0           1            2,790
## 2                 1                0           1            1,740
## 3                 1                1           2            1,260
## 4                 1                1           2            1,260
## 5                 1                1           2            1,583
## 6                 1                0           1            3,867
##   GROSS.SQUARE.FEET YEAR.BUILT TAX.CLASS.AT.TIME.OF.SALE
## 1             1,376       1940                         1
## 2             1,782       1960                         1
## 3             1,440       1940                         1
## 4             1,440       1930                         1
## 5             2,052       1920                         1
## 6             3,122       1925                         1
##   BUILDING.CLASS.AT.TIME.OF.SALE SALE.PRICE  SALE.DATE
## 1                             A1         $0 2011-02-08
## 2                             A5   $610,000 2011-10-24
## 3                             S1         $0 2011-07-11
## 4                             S1   $468,000 2011-06-13
## 5                             S1         $0 2011-11-11
## 6                             A1   $751,000 2011-04-19
```


```r
summary(bk)
```

```
##     BOROUGH                     NEIGHBORHOOD  
##  Min.   :3   BEDFORD STUYVESANT       : 1365  
##  1st Qu.:3   BOROUGH PARK             : 1046  
##  Median :3   WILLIAMSBURG-NORTH       : 1013  
##  Mean   :3   CROWN HEIGHTS            :  797  
##  3rd Qu.:3   BAY RIDGE                :  704  
##  Max.   :3   PARK SLOPE               :  668  
##              (Other)                  :15133  
##                                  BUILDING.CLASS.CATEGORY
##  02  TWO FAMILY HOMES                        :4791      
##  13  CONDOS - ELEVATOR APARTMENTS            :3118      
##  01  ONE FAMILY HOMES                        :2364      
##  03  THREE FAMILY HOMES                      :1766      
##  10  COOPS - ELEVATOR APARTMENTS             :1672      
##  07  RENTALS - WALKUP APARTMENTS             :1427      
##  (Other)                                     :5588      
##  TAX.CLASS.AT.PRESENT     BLOCK           LOT         EASE.MENT     
##  1      :9005         Min.   :  27   Min.   :   1.0   Mode:logical  
##  2      :6075         1st Qu.:1687   1st Qu.:  24.0   NA's:20726    
##  4      :2440         Median :3429   Median :  53.0                 
##  2A     :1170         Mean   :3999   Mean   : 380.2                 
##  2C     : 927         3rd Qu.:6339   3rd Qu.:1008.0                 
##  2B     : 379         Max.   :8955   Max.   :9039.0                 
##  (Other): 730                                                       
##  BUILDING.CLASS.AT.PRESENT
##  R4     : 3114            
##  C0     : 1767            
##  B1     : 1679            
##  D4     : 1669            
##  R5     : 1118            
##  B3     : 1056            
##  (Other):10323            
##                                       ADDRESS          APARTMENT.NUMBER
##  22 NORTH 6TH   STREET                    :  258               :14216  
##  2 NORTHSIDE PIERS                        :  148   4           :  224  
##  34 NORTH 7TH   STREET                    :  127   3           :  162  
##  189 SCHEMERHORN STREET                   :  120   6           :  161  
##  163 WASHINGTON AVENUE                    :  106   2           :  138  
##  80 METROPOLITAN AVENUE                   :   96   2B          :  130  
##  (Other)                                  :19871   (Other)     : 5695  
##     ZIP.CODE     RESIDENTIAL.UNITS COMMERCIAL.UNITS   TOTAL.UNITS     
##  Min.   :    0   Min.   :  0.00    Min.   : 0.0000   Min.   :  0.000  
##  1st Qu.:11211   1st Qu.:  1.00    1st Qu.: 0.0000   1st Qu.:  1.000  
##  Median :11218   Median :  1.00    Median : 0.0000   Median :  1.000  
##  Mean   :11217   Mean   :  2.36    Mean   : 0.1918   Mean   :  2.551  
##  3rd Qu.:11229   3rd Qu.:  2.00    3rd Qu.: 0.0000   3rd Qu.:  2.000  
##  Max.   :11416   Max.   :534.00    Max.   :43.0000   Max.   :536.000  
##                                                                       
##  LAND.SQUARE.FEET GROSS.SQUARE.FEET   YEAR.BUILT  
##  0      :8120     0      : 8887     Min.   :   0  
##  2,000  :1780     3,000  :  172     1st Qu.:1905  
##  2,500  : 925     2,400  :  159     Median :1928  
##  1,800  : 459     2,700  :  150     Mean   :1694  
##  4,000  : 367     3,600  :  134     3rd Qu.:1960  
##  2,003  : 322     3,300  :  119     Max.   :2012  
##  (Other):8753     (Other):11105                   
##  TAX.CLASS.AT.TIME.OF.SALE BUILDING.CLASS.AT.TIME.OF.SALE    SALE.PRICE   
##  Min.   :1.000             R4     : 3118                  $0      : 7421  
##  1st Qu.:1.000             C0     : 1766                  $10     :  220  
##  Median :2.000             B1     : 1673                  $450,000:  121  
##  Mean   :1.767             D4     : 1669                  $550,000:  117  
##  3rd Qu.:2.000             R5     : 1115                  $400,000:  114  
##  Max.   :4.000             B3     : 1061                  $250,000:  104  
##                            (Other):10324                  (Other) :12629  
##       SALE.DATE    
##  2011-06-27:  225  
##  2011-05-11:  180  
##  2011-06-29:  178  
##  2011-10-06:  149  
##  2011-12-22:  139  
##  2011-01-31:  137  
##  (Other)   :19718
```


```r
str(bk)
```

```
## 'data.frame':	20726 obs. of  21 variables:
##  $ BOROUGH                       : int  3 3 3 3 3 3 3 3 3 3 ...
##  $ NEIGHBORHOOD                  : Factor w/ 61 levels "BATH BEACH               ",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ BUILDING.CLASS.CATEGORY       : Factor w/ 37 levels "01  ONE FAMILY HOMES                        ",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ TAX.CLASS.AT.PRESENT          : Factor w/ 11 levels "  ","1","1A",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ BLOCK                         : int  6373 6380 6399 6399 6408 6412 6413 6431 6433 6442 ...
##  $ LOT                           : int  88 71 4 7 48 31 20 5 10 131 ...
##  $ EASE.MENT                     : logi  NA NA NA NA NA NA ...
##  $ BUILDING.CLASS.AT.PRESENT     : Factor w/ 124 levels "  ","A0","A1",..: 3 7 101 101 101 3 3 9 7 101 ...
##  $ ADDRESS                       : Factor w/ 15211 levels "1 CAMBRIDGE PLACE                        ",..: 14625 14232 3806 3768 5038 14278 1277 3685 3945 5232 ...
##  $ APARTMENT.NUMBER              : Factor w/ 1491 levels "            ",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ ZIP.CODE                      : int  11214 11214 11214 11214 11214 11214 11214 11214 11214 11214 ...
##  $ RESIDENTIAL.UNITS             : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ COMMERCIAL.UNITS              : int  0 0 1 1 1 0 0 0 0 1 ...
##  $ TOTAL.UNITS                   : int  1 1 2 2 2 1 1 1 1 2 ...
##  $ LAND.SQUARE.FEET              : Factor w/ 2255 levels "0","1,000","1,003",..: 1244 419 113 113 304 1647 1938 295 214 2098 ...
##  $ GROSS.SQUARE.FEET             : Factor w/ 3015 levels "0","1","1,000",..: 194 458 227 227 872 1676 1882 1124 1193 94 ...
##  $ YEAR.BUILT                    : int  1940 1960 1940 1930 1920 1925 1915 1930 1937 1925 ...
##  $ TAX.CLASS.AT.TIME.OF.SALE     : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ BUILDING.CLASS.AT.TIME.OF.SALE: Factor w/ 124 levels "A0","A1","A2",..: 2 6 101 101 101 2 2 8 6 101 ...
##  $ SALE.PRICE                    : Factor w/ 3347 levels "$0","$1","$1,000",..: 1 2558 1 2027 1 2934 1 2387 1 1 ...
##  $ SALE.DATE                     : Factor w/ 355 levels "2011-01-01","2011-01-02",..: 39 288 188 160 306 106 168 73 259 195 ...
```

<br>


#### Follow the steps below to tidy the data
The steps below will load remove the header data form the file, clean/format the data and remove zero sale price data. 
<br>
<br>

#### Step 1 - Clean and format the data with regular expressions. In this step we will transform the data by changing numeric values to a factor, changing all variables to lower case, remove leading digits, and change formatting of dates.
````````````
Change Sales price from numeric to a factor

bk$SALE.PRICE.N <- as.numeric(gsub("[^[:digit:]]","", bk$SALE.PRICE))
count(is.na(bk$SALE.PRICE.N))


Transform all variables to lower case

names(bk) <- tolower(names(bk)) 


Remove leading digits

bk$gross.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$gross.square.feet))
bk$land.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$land.square.feet))


Change sale.date to a date format in R

bk$sale.date <- as.Date(bk$sale.date)
bk$year.built <- as.numeric(as.character(bk$year.built))
````````````


```r
knitr::opts_chunk$set(cache=TRUE)

bk$SALE.PRICE.N <- as.numeric(gsub("[^[:digit:]]","", bk$SALE.PRICE))

count(is.na(bk$SALE.PRICE.N))
```

```
##       x  freq
## 1 FALSE 20726
```

```r
names(bk) <- tolower(names(bk)) 

bk$gross.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$gross.square.feet))

bk$land.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$land.square.feet))

bk$sale.date <- as.Date(bk$sale.date)

bk$year.built <- as.numeric(as.character(bk$year.built))
```


