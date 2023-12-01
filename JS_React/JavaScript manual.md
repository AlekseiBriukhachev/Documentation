# JavaScript and React

## Содержание

[1 Подготовка к работе](#1-подготовка-к-работе)<br>
[1.1 Конфигурация VSCode](#11-конфигурация-vscode)<br>
[1.2 Конфигурация ESInt](#12-конфигурация-eslint)<br>
[2 Основы JavaScript](#2-основы-javascript)<br>
[2.1 Команды](#21-команды)<br>
[2.2 Функции, стрелочные функции](#22-функции-стрелочные-функции)<br>
[2.3 Методы и свойства строк и чисел](#23-методы-и-свойства-строк-и-чисел)<br>
[2.4 Callback функция](#24-callback-функция)<br>
[2.5 Объекты, деструктуризация объектов](#25-объекты-деструктуризация-объектов)<br>
[2.6 Массивы и псевдомассивы](#26-массивы-и-псевдомассивы)<br>

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
|str.trim()|Отрезает пробелы в строке|
|Math.round(num)|Округление числа до ближайшего целого|
|parseInt(str)|Парсование целого числа из начала и конца строки|
|parseFloat(str)|Парсование числа с плавающей точкой из строки|

### 2.4 Callback функция

Callback - это функция, которая должна быть выполнена после того, как другая функция завершила свое выполнени.

Главный шаблон callback функции:

```JavaScript
function learnJS(lang, callback) {
    console.log(`I learn: ${lang}`);
    callback();
}

function done() {
    console.log('I finish this class');
}

learnJS('JavaScript', done);
```

### 2.5 Объекты, деструктуризация объектов

Создание объекта:

```JavaScript
const options = {
    name: 'test',
    width: 1024,
    hegth: 1024,
    colors: {
        border: 'black',
        bg: 'red;
    },
    makeTest: function() {
        console.log('test');
    }
};

//Запуск метода, встроенного в объект
options.makeTest();
```

Удаление поля из объекта:

```JavaScript
delete options.name;
```

Просмотр свойств (полей объекта):

```JavaScript
for (let key in options) {
    if (typeof(options[key]) === 'object') {
        for (let i in options[key]) {
            console.log(`Option ${i} has value ${options[key][i]}`);
        }
    } else {
        console.log(`Option ${key} has value ${options[key]}`);
    }
};
```

У объекта есть метод (часто используемый) **Оbject.keys()** - выводит количество полей объекта.

```JavaScript
Object.keys(options).length;
```

**Деструктуризация объекта:**

```JavaScript
const {border, bg} = options.colors;
console.log(border);
console.log(bg);
```

### 2.6 Массивы и псевдомассивы

Метод для работы с концом массива:

```JavaScript
const arr = [1, 2, 3, 5, 8, 9];
arr.pop(); //удаляет последний элмент массива
arr.push(10); //добавляет элемент в конец массива
```

Существуют методы для вставки и удаления элементов в начало масива, это методы **shift()** и *unshift()**. Но из-за того, что при вставке и удалении элементов приходится менять нумерацию индексов всех элементов (что занимает много времени), эти методы практически не используются.

Для перебора всех элементов масива используется чаще всего цикл **for(){}**:

```JavaScript
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
// можно еще использовать такой цикл для перебора элементов
for (let value of arr) {
    console.log(value);
}
```

Метод массива **forEach()** принимает параметром callback функцию:

```JavaScript
arr.forEach(function(element, i, arr) {
    console.log(`${i}: ${element} inside array ${arr}`);
});
```

Сallback функция может принимать 3 аргумента:

1. Первый аргумент - это тот злемент, который мы сейчас перебираем.
2. Второй аргумент - номер по порядку.
3. Третий аргумент - ссылка на массив, который мы перебираем.

Методы Объекта и массива
![Методы Объекта и массива](/JS_React/img/Objects_Arrays.jpg)

[Отличия for...of от for...in](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/for...of#%D1%80%D0%B0%D0%B7%D0%BB%D0%B8%D1%87%D0%B8%D1%8F_%D0%BC%D0%B5%D0%B6%D0%B4%D1%83_for...of_%D0%B8_for...in)

Методы **split(), join(), sort()**

Метод **split()** разделяет одну строку по какому-то делимитеру, и создает массив отдельных слов.

```JavaScript
const str = prompt('', '');
const products = str.split(', ');
```

Метод **join()** - это обратная операция, т.е. на основе массива строк создает целое предложение.

```JavaScript
const str = prompt('', '');
const products = str.split(', ');
console.log(products.join('; '))
```

Метод **sort()** - это метод сортировки. Сортирует все как строки, по первому символу.

```JavaScript
const str = prompt('', '');
const products = str.split(', ');
products.sort();
console.log(products.join('; '))
```

Данный метод может принимать callback функцию, в которой можно указать, как должна выполняться сортировка.

```JavaScript
const arr = [1, 2, 4, 6, 10];
arr.sort(compareNum);
console.log(arr);

function compareNum(a, b) {
    return a - b;
}
```

[Алгоритм быстрой сортировки](https://algolist.ru/sort/quick_sort.php)

Псевдомассивы - это объект, структура которого совпадает со структурой массива, но у таких псевдомассивов нет никаких методов.
[Алгоритмы поиска на JavaScript](https://web.archive.org/web/20221025084508/http://mathhelpplanet.com/static.php?p=javascript-algoritmy-poiska)