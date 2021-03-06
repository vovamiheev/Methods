1. Створити матрицю mat з 5 стовпцями та 10 строками за допомогою matrix з випадковими даними (функція rnorm(50)).

```r
 mat <- matrix(rnorm(50), nrow = 10, ncol = 5)
```
2. Знайти максимальне значення в кожному стовпці.

```r
apply(mat, MARGIN = 2, max)

[1] 1.3447103 1.2991105 0.7473742 2.0892833 1.6879483
```

3. Знайти середнє (mean) значення кожного стовпця.

``` r
apply(mat, MARGIN = 2, mean)

[1] -0.23670639  0.09223969 -0.25572853 -0.08331463  0.22539212
```
4. Знайти мінімальне значення в кожному рядку.

``` r
apply(mat, MARGIN = 1, min)

[1] -0.3375536 -1.2266173 -0.4876943 -2.5285830 -2.0454051 -0.7940537
 [7] -1.8420149 -1.0945650  0.2605482 -0.8539102
``` 

5. Відсортувати кожен стовбець таблиці.

``` r
apply(mat, MARGIN = 2, sort)

 [,1]        [,2]       [,3]        [,4]        [,5]
 [1,] -1.8420149 -1.09456498 -2.5285830 -2.04540510 -0.85391019
 [2,] -1.2857627 -0.76775232 -0.7940537 -1.22661731 -0.33755358
 [3,] -0.9039987 -0.60598992 -0.5074539 -0.60104366  0.06401433
 [4,] -0.4876943  0.02860126 -0.4501879 -0.43664309  0.12017627
 [5,] -0.4460200  0.16386525 -0.3249227 -0.34199616  0.16399499
 [6,] -0.1862805  0.30847333 -0.3042922 -0.23582779  0.18536697
 [7,] -0.1517508  0.41235012  0.5118944  0.08058327  0.26054815
 [8,]  0.3619476  0.50934972  0.5406364  0.60855498  0.39556053
 [9,]  1.2298003  0.66895395  0.5523031  1.27596527  0.56777546
[10,]  1.3447103  1.29911051  0.7473742  2.08928334  1.68794832
```
6. Знайти кількість значень < 0 для кожного стовпця. Використати свою функцію.

``` r
count_negative_values <- function (y) {
  i <- 1
  negative_values <- 0
  
  for (i in 1:length(y)){
    if (y[i] < 0) {
      negative_values <- negative_values + 1
    }
    i <- i + 1
  }
  negative_values
}

apply(mat, MARGIN = 2, count_negative_values)

[1] 7 3 6 6 2
``` 

7. Вивести вектор з булевими значеннями TRUE та FALSE. TRUE, якщо в стовпці є елементи >2, FALSE – якщо немає.

``` r
is_bigger_2 <- function (y) {
  if (any(y > 2)) {
    result <- TRUE
  } else {
    result <- FALSE
  }  

  result
}

apply(mat, MARGIN = 2, is_bigger_2)

[1] FALSE FALSE FALSE  TRUE FALSE
```
