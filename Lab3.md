1.За допомогою download.file() завантажте любий excel файл з порталу http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.

```r                                   
library(readxl)
download.file('https://data.gov.ua/dataset/85e5e66c-be8b-4e75-a7df-d3e4c886fa73/resource/9e4066f7-4a81-4430-86e2-9f2abfe5dd45/download/129-indeks-produktsiyi-tvarinnitstva-narostaiuchim-pidsumkom-u-2019-rotsi-z-pochatku-roku-do-vi.xlsx', mode='wb', destfile='lab1_1.xlsx');
data1 <- read_excel('lab1_1.xlsx', sheet=1);
head(data1, 6);
```  


    ## A tibble: 6 x 4   code         title       description                           datatype                                      
                        1 code         коди        00 - господарства усіх категорій; 10… string  
                        2 date         дата        Дата у форматі ISO 8601 (рррр-мм-дд)… date     
                        3 data         дані        "Індекс продукції  тваринництва наро… decimal  
                        4 Unit of mea… Одиниця ви… %                                     NA       
                        5 note         Примітка    Дані наведено без урахування тимчасо… NA       
                        6 note         Примітка    Річні дані за 2019 рік попередні.     NA
                                                                                                          
2.За допомогою download.file() завантажте файл getdata_data_ss06hid.csv за посиланням https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0 Необхідно знайти, скільки property мають value $1000000+.
```r                                                                                                                                      
download.file('https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv', destfile='lab1_2.csv');
data_2 <- read.csv("lab1_2.csv")
sum(data_2$VAL == 24, na.rm = TRUE)
```
    ## [1] 53                          
3.Зчитайте xml файл за посиланням http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml. Скільки ресторанів мають zipcode 21231?
```r  
library(XML)                                                         
xml <- xmlTreeParse("http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml",useInternal=TRUE)
node <- xmlRoot(xml)
length(xpathApply(node, '//row/row/zipcode[text()="21231"]'))
``` 
    ## [1] 127
