Лабораторна робота № 5. Зчитування даних з WEB.
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
[1] "Джентльмени"         "Ножі наголо"         "Джокер"             
[4] "Джуді"               "Sound of Metal"      "Месники: Завершення"
```
---------------------

2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
```r                        
> movies[movies$Runtime > 120, ]$Title
   [1] "Ножі наголо"                                  
 [2] "Джокер"                                       
 [3] "Sound of Metal"                               
 [4] "Месники: Завершення"                          
 [5] "Одного разу... в Голлівуді"                   
 [6] "Паразити"                                     
 [7] "Аутсайдери"                                   
 [8] "Судити по совісті"                            
 [9] "Доктор Сон"                                   
[10] "Сонцестояння"                                 
[11] "Термінатор: Фатум"                            
[12] "Сирота Бруклін"                               
[13] "Джуманджі: Наступний рівень"                  
[14] "Маленькі жінки"                               
[15] "Зоряні війни: Епізод 9 - Скайвокер. Сходження"
[16] "Воно 2"                                       
[17] "Неограновані коштовності"                     
[18] "Ірландець"                                    
[19] "Король"                                       
[20] "Мідвей"                                       
[21] "Людина-павук: Далеко від дому"                
[22] "A Call to Spy"                                
[23] "Аліта: Бойовий ангел"                         
[24] "Капітан Марвел"                               
[25] "Аладдін"                                      
[26] "Портрет дівчини у вогні"                      
[27] "Річард Джуелл"                                
[28] "6 футів під землею"                           
[29] "Форсаж: Гоббс та Шоу"                         
[30] "Джон Вік 3"                                   
[31] "До зірок"                                     
[32] "Ґодзілла II: Король Монстрів"                 
[33] "Шлюбна історія"                               
[34] "Рокетмен"                                     
[35] "Шазам!"                                       
[36] "Скло"                                         
[37] "Темні води"                                   
[38] "Operation Brothers"                           
[39] "Падіння янгола"                               
[40] "Приховане життя"                              
[41] "El Camino: A Breaking Bad Movie"              
[42] "Абатство Даунтон"                             
[43] "Правдива історія банди Келлі"
```
---------------------

3. Скільки фільмів мають тривалість менше 100 хв.
```r                  
> length(movies[movies$Runtime < 100, ]$Title)
[1] 21
```
