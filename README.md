### Задание

С сайта dzen news (https://dzen.ru/news) необходимо
собрать краткий текст и названия всех статей за последний месяц (на момент выполнения) с ключевым словом "игра".
Затем для полученных статей необходимо рассчитать топ-50 наиболее частотных слов и представить их в виде word (tag) cloud.
Данное задание необходимо выполнить с помощью python.
Для представления в виде word cloud можно использовать уже существующие библиотеки.


### Описание

Программа состоит из двух классов: 1) Parser, 2) Process

#### 1) **Класс Parser** представляет собой асинхронный парсер, который состоит из следующих функций.

   1. Функция get_links_cards

   В этой функции собираются ссылки на все статьи с сайта dzen.ru

   2. Функция get_texts 

   В этой функции извлекаются все необходимые данные из каждой статьи (заголовок и основной текст), а также каждому тексту присваивается индекс

   3. Функция main 

   Эта функция служит точкой входа в event loop, в ней создаются задачи для их дальнейшего асинхронного выполнения.

   Все полученные тексты записываются в файл texts_row.json в следующем виде:

   {
        "index": 1,
        "title": "Госдолг США обновил исторический максимум и превысил $33,442 трлн",
        "body": [
            "Государственный долг США составил 33,442 триллиона долларов.",
            "Год назад долг США вырос на 195 миллиардов долларов, а на прошлой неделе увеличился на 10 миллиардов долларов.",
            "Одновременно американский долг перед физлицами, бизнесом и остальным миром вырос примерно на 9 миллиардов долларов.",
            "В то же время российский госдолг на 1 сентября составлял 25,6 триллиона рублей, или 267,3 миллиарда долларов."
        ]
    }

#### 2) **Класс Process.** В этом классе полученные тексты обрабатываются и сортируются по наличию в них слова "игра". 
   Класс состоит из следующих функций:
   
   1. Функция lemmatize_texts
      
      В этой функции все тексты лемматизируются с помощью библиотеки PyMystem3
   
   2. Функция check_lemmatized_texts
     
      Эта функция отбирает из уже лемматизированных текстов только те, в которых содержится слово "игра"

   3. Функции make_onedim_array и count_words
     
      В этих функциях текст приводится к формату str, а также подсчитываются наиболее частотные слова в отобранных текстах. 
      Функция возвращает набор наиболее частотных слов из текстов со словом "игра"

**По итогу работы обоих классов возвращаются три файла**:

texts_row - общий список текстов с сайта dzen.ru
texts_games - список текстов, в которых есть слово "игра"
texts_sorted - список лемматизированных текстов, в которых есть слово "игра"
top_words - набор наиболее частотных слов из текстов со словом "игра"

Полученные слова можно загрузить на [сервис](https://wordscloud.pythonanywhere.com/) для формирования облака из слов

**Небольшое (важное) примечание**. По итогу спарсить статьи именно за последний месяц не получилось, поскольку на dzen.ru нет ни сортировки по датам, ни пагинации. 
Через AJAX подгружается лишь ограниченное число статей. Как итог, удалось спарсить только все статьи на главной страницу, это около 70. Но данная программа подходит для любого количества статей.

Ссылка на класс Process из google-colab, там он работает гораздо быстрее по очевидным причинам [ссылка](https://colab.research.google.com/drive/1NPWCp7Nr91t2Vofb7LPHmA6izD2MqNjw#scrollTo=JMWZZSGb-J0P)



