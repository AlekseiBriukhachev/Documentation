# JavaScript and React

### Содержание

[1 Подготовка к работе](#1-подготовка-к-работе)<br>
[1.1 Конфигурация VSCode](#11-конфигурация-vscode)<br>
[1.2 Конфигурация ESInt](#12-конфигурация-eslint)<br>
[2 Основы JavaScript](#2-основы-javascript)<br>
[2.1 Команды](#21-команды)<br>

## 1 Подготовка к работе

### 1.1 Конфигурация VSCode

It is usefull to confugurate IDE.
It needs some plugins:

- All autocomplete
- Auto Close Tag
- Auto Complete Tag
- Code Runner
- Import Cost
- JavaScript (ES6) code snippets
- Live Server
- Sass
- Theme — Oceanic Next
- VSCode-icons
- React code snipped
- jshint
- ESLint

Manager of packages npm. Needs to install Node.js from official site nodejs.org.

### 1.2 Конфигурация ESlint

1. ESInt is check of code during proramming: logic errors or somthing like this. It checks all mistakes automaticaly.

1. Install this plugin.
[ESLint dokumentation](https://eslint.org/) installation with maneger of packages **npm**.

`npm init @eslint/config`

2 Атвоматическое форматирование при сохранении файла:

- settings -> Editor format on save
![Alt text](/JS_React/img/default_formatter.png)
            -> default formatter
            ![Alt text](/JS_React/img/formt_on_save.png)
            -> settings JSON ![Alt text](/JS_React/img/json_conf.png)

## 2 Основы JavaScript

### 2.1 Команды

|Comands|Description|
|-:|:-|
|console.log()|Вывод в консоль|
|alert()|Вывод на экран в выпадающее окно|
|confirm()|Выпадающее окно да/нет -> результат boolean|
|prompt('текст', '\<placeholder>')|Выпадающее окно с текстом наример вопрос с выбором вариантов ответов и строкой ввода. Результат текст введеный в строке ввода.|
|typeof(var)|Проверяет тип данных|
|document.write()|Выписывает какие-то данные прямо на странице|
|${*some_variable*}|Интерполяция - динамическое использование переменных, констант|


### 2.2 Функции, стрелочные функции

Синтаксис:

Сначала пишется ключевое слово **function** мы говорим, что это функция. После идет какое-то название, например *showFirstMessage**. Потом идут фигурные скобки - тело функции. Там прописываются какие-то действия. Чтобы она заработала, ее необходи вызвать. Мы обращаемся к имени функции и стивим круглые скобки.

В функцию могут быть переданы какие-то параметры, которые данная функция будет использовать внитри себя. Функция может менять значение глобальной переменной. Замыкание функции - функция приобработке переменных ищет эти переменные сначала внутри себя, ели не находит, идет на уровень выше, и т.д. Замыкание функции - это сама функция вместе со всеми переменными, которые ей доступные.

Возвращение значения функцией: 
```JavaScript
function calc(a, b) {
    return (a + b);
}
```

Классификация функций:
![Alt text](/JS_React/img/classif_func.png)

### 2.3 Методы и свойства строк и чисел

[Документация по JavaScript](https://learn.javascript.ru/)

|Метод|Описание|
|-:|:-|
|str.length|Длина строки|
|arr.length|Длина массива|
|str[2]|Получение элемента по индексу|
|str.toUpperCase()|Преобразовать строку в заглавные буквы. Возвращает новое значение|
|str.toLowerCase()|Преобразовать строку в нижний регистр. Возвращает новое значение|
|str.indexOf("substring")|Выводит индекс позиции, с которой начинается это слово переданное в параметре метода|
|str.slice(6, 11)|Выводит на экран кусок строки. Первый параметр - с какого индекса начинать, второй параметр - по какой индекс вырезать|
|str.substring(6, 11)|Выводит на экран кусок строки. Первый параметр - с какого индекса начинать, второй параметр - по какой индекс вырезать. Не поддерживает отрицательныйе значения параметров в отличии от `slice()`|
|str.substr(6, 11)|Выводит на экран кусок строки. Первый параметр - с какого индекса начинать, второй параметр - длина строки, количество символов.|
|Math.round(num)|Округление числа до ближайшего целого|
|parseInt(str)|Парсование целого числа из строки|
|parseFloat(str)|Парсование числа с плавающей точкой из строки|