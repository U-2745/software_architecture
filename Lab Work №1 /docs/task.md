Для работы был выбран прецедент "Сохранение результата в аккаунте"
## Диаграммы компонентов
Были развернуты контейнеры:
#### Модуль авторизации
![auth](https://github.com/U-2745/software_architecture/assets/78296925/0b34e644-ff05-4076-8e96-ab7ed771f35f)

#### Модуль сохранения результатов на сервере
![savingresults](https://github.com/U-2745/software_architecture/assets/78296925/0fc4f0c4-1b2c-407f-9c74-36ebaddda8e3)

## Диаграмма последовательностей
[sequence](https://github.com/U-2745/software_architecture/assets/78296925/c284fcb2-27e3-475b-beba-fb17379fb509)

## Модель БД в виде диаграммы классов
![database](https://github.com/U-2745/software_architecture/assets/78296925/72bbf112-3ede-4ba0-b014-7e8154f48b9f)

## Использование принципов KISS, YAGNI, DRY и SOLID в коде
Для реализации системы используется python.
### KISS
Keep it simple, stupid / Сделай это просто и понятно
Код читается просто, используются простые методы
```
def validate_language(input):
    res = False
    tc = nltk.classify.textcat.TextCat() 
    language = tc.guess_language(input)
    if (language in ['English', 'Russian']): res = True
    return res
```

### YAGNI
You aren't gonna need it / Вам это не понадобится
Используются только нужные библиотеки
```
import pandas
import TextBlob
import NLTK
import pymorphy2
```

### DRY 
Don't repeat yourself / Не повторяйся
Для формирования красивой строки пользователю на вывод из словаря выявленных форм/цветов/эмоций используется один метод, а не три разных
```
def format_params(dict):
    res = str()
    for key in dict:
        res += key + ": " + dict[key] + ", "
    res = res[:-1]
    return res
```

### SRP
Single responsibility principle / Принцип единственной ответственности
Для проверки текста, его нормализации, анализа текста, выделения форм, генерации результата использованы разные методы
```
def validate_input_length_(input)
  ...
def validate_input_language(input)
  ...
def normalize_input(input)
  ...
def extract_sentiment(normalized_text)
  ...
def extract_moods(normalized_text)
  ...
def define_shapes(extracted_sentiment, extracted_moods)
  ...
def define_colors(extracted_sentiment, extracted_moods)
  ...
def generate_output(defined_shapes, defined_colors)
  ...
def form_pdf(generated_output)
  ...
```
