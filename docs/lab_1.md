# Лабораторная работа №1: Формулирование требований к программной системе

**Цель работы:** Научиться анализировать поставленную задачу, формулировать функциональные и нефункциональные требования к проектируемой системе.

## Перечень заинтересованных лиц (стейкхолдеров) с краткими описаниями (2 балла)
1.	Научный руководитель.
   
Заинтересован в результате, имеющем полный функционал в заданные сроки.

2.	Продвинутые пользователи.
   
Гейм-дизайнеры и концепт-художники. Заинтересованы в постоянной работе веб-приложения, важна возможность сохранять результат и перегенерировывать его.

3.	Любопытствующие пользователи.
   
Пользователи, которые используют ресурс в развлекательных и/или личных целях, заинтересованы в быстром и «цепляющем» результате.
## Перечень функциональных требований (2 балла)
1.  Ввод текста

    1.1. вставка текста из буфера обмена
    
    1.2. загрузка файла с расширением .txt, .doc, .docx
    
2.  Получение результата работы

3.  Работа с результатом
   
    3.1. копирование результата по кнопке "Скопировать"
    
    3.2. сохранение результата локально в виде PDF-файла

## Диаграмма вариантов использования для функциональных требований (2 балла)

## Перечень сделанных предположений (всё, что не оговорено в постановке явно можно “додумать” самостоятельно) (2 балла)
- «Любопытствующие пользователи» как стейкхолдеры

- Интересы стейкхолдеров
  
- Возможность загрузить текстовый файл на вход

- Наличие кнопки "Скопировать" для выходного результата
  
- Максимальное количество пользователей в моменте – 10000


## Перечень нефункциональных требований (2 балла)
- Система должна быть способна до 10000 пользователей в момент времени без снижения производительности.

- Система должна иметь возможность увеличивать масштаб по мере необходимости.

- Система должна работать на разных платформах с минимальными изменениями.

- Система должна быть простой и понятной в использовании.