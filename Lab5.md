Лабораторна робота № 3. Зчитування даних з WEB.
================

В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі 100 фільмами 2019 року виходу за посиланням «http://www.imdb.com/search/title?count=100&release_date=2019,2017&title_type=feature». Необхідно створити data.frame «movies» з наступними даними: номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data). Для виконання лабораторної рекомендується використати бібліотеку «rvest». CSS селектори для зчитування необхідних даних: rank_data: «.text-primary», title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для зчитування url використовується функція read_html, для зчитування даних по CSS селектору – html_nodes і для перетворення зчитаних html даних в текст - html_text. Рекомендується перетворити rank_data та runtime_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».


```r
> install.packages("rvest")
> library('rvest')
> library('xml2')
> html <- read_html("http://www.imdb.com/search/title?count=100&release_date=2019,2019&title_type=feature")
> install.packages('selectr')
> rank_html <- rvest::html_nodes(html,'.text-primary')
> rank_data <- rvest::html_text(html)
> rank_data <- as.numeric(rank_data)
> title_html <- html_nodes(html,'.lister-item-header a')
> title_data <- html_text(title_html)
> runtime_html <- html_nodes(html,'.text-muted .runtime')
> runtime_data <- html_text(runtime_html)
> runtime_data <- gsub(" min", "", runtime_data)
> runtime_data <- as.numeric(runtime_data)
> movies <- data.frame(Rank = rank_data, Title = title_data, Runtime = runtime_data, stringsAsFactors = FALSE)
```

---------------------

1. Виведіть перші 6 назв фільмів дата фрейму
```r
> head(movies$Title, 6)

```
---------------------

2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
```r                        
> movies[movies$Runtime > 120, ]$Title
   
```
---------------------

3. Скільки фільмів мають тривалість менше 100 хв.
```r                  
> length(movies[movies$Runtime < 100, ]$Title)

```
