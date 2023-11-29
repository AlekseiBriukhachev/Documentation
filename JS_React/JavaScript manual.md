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


### 2.2 Операторы

|Operator|Description|
|-:|:-|
|