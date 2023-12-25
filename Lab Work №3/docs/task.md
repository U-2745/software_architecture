Для работы был выбран прецедент "Сохранение результата в аккаунте"
## Диаграммы компонентов
Были развернуты контейнеры:
#### Модуль авторизации
![auth](https://github.com/U-2745/software_architecture/assets/78296925/15190206-c067-45fd-a6fe-776e7d578414)

#### Модуль сохранения результатов на сервере
![savingresults](https://github.com/U-2745/software_architecture/assets/78296925/17dd36cb-6eb2-4a4a-8fc0-5bfb171b569e)

## Диаграмма последовательностей
![sequence](https://github.com/U-2745/software_architecture/assets/78296925/44dee8bf-7c7b-490f-bf5c-e48c66dacc41)

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
### SOLID
#### SRP
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

#### OCP
Open closed principle / Принцип открытости-закрытости

В проекте не предусмотрено создание классов, которые позже можно будет изменять и дополнять, поэтому прнцип отразить не получится.

#### LSP
Liskov substitution principle / Принцип подстановки Барбары Лисков

В базовый класс были вынесены только те методы, которые характеры всем его наследникам.

#### ISP
Interface segregation principle / Принцип разделения интерфейсов

В проекте не предусмотрено использование интерфейсов, поэтому прнцип отразить не получится.

#### DIP
Dependency inversion principle / Принцип инверсии зависимостей

В проекте классы не полагаются напрямую на другие классы, а зависят от абстракций.
```
class TextAnalyzer(normalized_text):
    def __init__(self, normalized_text):
        self.text = normalized_text
    
    def extract_moods(self, normalized_text):
        # логика выделения настроений текста
        return extracted_moods

    def extract_sentiment(self, normalized_text):
        # логика выделения эмоциональности текста
        return extracted_sentiment

class ParametersDefiner:
    def __init__(self, extracted_moods, extracted_sentiment):
        self.moods = extracted_moods
        self.emotionality = extracted_sentiment
```
