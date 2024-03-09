# 4. Продвинутый JavaScript

[4.1 Локальные сервера](#41-локальные-сервера)<br>
[4.2 JSON](#42-json)<br>
[4.3 AJAX и общение с сервером](#43-ajax-и-общение-с-сервером)<br>
[4.4 Promise](#44-promise)<br>
[4.5 Fetch API](#45-fetch-api)<br>
[4.6 Методы перебора массивов](#46-методы-перебора-массивов)<br>
[4.7 npm проект. json-server](#47-npm-проект-json-server)<br>
[4.8 Получение данных с сервера. Async/Await](#48-получение-данных-с-сервера-asyncawait)<br>
[4.9 Библиотека Axios](#49-библиотека-axios)<br>
[4.10 Сохранение данных без БД. Работа с localStorage](#410-сохранение-данных-без-бд-работа-с-localstorage)<br>
[4.11 Геттеры и сеттеры](#411-геттеры-и-сеттеры)<br>
[4.12 Инкапсуляция](#412-инкапсуляция)<br>
[4.13 Webpack](#413-webpack)<br>
[4.14 Babel](#414-babel)<br>
[4.15 Библиотеки и фреймворки](#415-библиотеки-и-фреймворки)<br>
[4.16 Библиотека jQuery](#416-библиотека-jquery)<br>
[Какие проекты можно придумать и реализовать самостоятельно](#Какие-проекты-можно-придумать-и-реализовать-самостоятельно)<br>

## 4.1 Локальные сервера

[MAMP](https://www.mamp.info/de/windows/)

[Open Server](https://ospanel.io/)

## 4.2 JSON

```JavaScript
const person = {
    name: 'Alex',
    tel: '+77973289237'
};

console.log(JSON.stringify(person)); // из объекта в JSON

console.log(JSON.parse(JSON.stringify(person))); // из JSON в объект

```

Создание глубоких копий

```JavaScript
const person = {
    name: 'Alex',
    tel: '+77973289237',
    parents: {
        mom: 'Olga',
        dad: 'Mike'
    }

    const clone = JSON.parse(JSON.stringify(person));// созданаие нового независимого объекта
    clone.parents.mom = 'Ann';
};
```

## 4.3 AJAX и общение с сервером

```JavaScript

const inputRub = document.querySelector('#rub'),
    inputUsd = document.querySelector('#usd');
```

событие 'change' подсвечивает input пока он выбран

`inputRub.addEventListener('change', () => {`

событие 'input' отслеживает пока активный 'input'

```JavaScript
inputRub.addEventListener('input', () => {
    //создается request
    const request = new XMLHttpRequest();
```

методы XMLHttpRequest

```JavaScript
    request.open(HttpMethod, url, asyncб
login, password
)
;
```

- собирает настройки, которые потом помогут сделать запрос
  AJAX запросы ао умолчанию являются асинхронными

```JavaScript
    request.open('GET', 'js/current.json');
```

установка headers

```JavaScript
    request.setRequestHeader('Content-type', 'application/json; charset=utf-8');
```

отпарвка запроса

```JavaScript
    request.send();
```

свойства запроса

- status - статус код
- statusText - сообщение
- response - ответ от сервера
- readyState - текущее состояние зарпоса
- 'readystatechange' - остлеживает готовность запроса в данный текущий момент
- `request.addEventListener('readystatechange', () => {` данный слушатель используется редко

```JavaScript
    request.addEventListener('load', () => {
    // if (request.readyState === 4 && request.status === 200) {
    if (request.status === 200) {
        console.log(request.response);
        const data = JSON.parse(request.response);
        inputUsd.value = (+inputRub.value / data.current.usd).toFixed(2);
    } else {
        inputUsd.value = 'что-то не то';
    }
});

})
;
```

## 4.4 Promise

Технология `Promise` - обещания, если произошло что-то, то мы обещаем, что выполним какое-то действие. И так по цепочке.
Пример **callback hell**:

```JavaScript
console.log('Запрос данных...');

setTimeout(() => {
    console.log('Подготовка данных...');

    const product = {
        name: 'TV',
        price: 2000
    };

    setTimeout(() => {
        product.status = 'ordered';
        console.log(product);
    }, 2000);
}, 2000);
```

А как будет выглядеть этот код с применением технологии `promise`:

```JavaScript
console.log('Запрос данных...');

const req = new Promise(function (resolve, reject) {
    setTimeout(() => {
        console.log('Подготовка данных...');

        const product = {
            name: 'TV',
            price: 2000
        };
        resolve(product);
    }, 2000);
}).then((product) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            product.status = 'ordered';
            resolve(product);
        }, 2000);
    });
}).then(data => {
    data.modify = true;
    return data;
}).then(data => {
    console.log(data);
}).catch(() => {
    console.error('Произошла ошибка');
    ;
}).finally(() => {
    console.log('Finally');
});
```

## 4.5 Fetch API

Для использования Fetch нужно записать `fetch()`

[Fetch Documentation](https://developer.mozilla.org/ru/docs/Web/API/Fetch_API/Using_Fetch)

[{JSON} Placeholder](https://jsonplaceholder.typicode.com)

Fetch использует промисы.

`GET` запросы

```JavaScript
fetch('https://jsonplaceholder.typicode.com/todos/1')
    .then(response => response.json())
    .then(json => console.log(json))
```

`POST` запросы - нужно сделать кое-какие настройки

```JavaScript
fetch('https://jsonplaceholder.typicode.com/posts', {
    method: "POST",
    body: JSON.stringify({name: 'Alex'}),
    headers: {
        'Content-type': 'application/json'
    }
})
    .then(response => response.json())
    .then(json => console.log(json))
```

## 4.6 Методы перебора массивов

1. Метод `forEach` не возвращает новый массив, просто берет существующий и перебирает все элементы массива.

2. Метод `filter` - фильтрует элементы внутри массива, возвращает новый массив

```JavaScript
const names = ['Ivan', 'Ann', 'Ksenia', 'Voldemart'];

// получить все имена, в которых количество элементов меньше 5
const =
shortNames = names.filter(function (name) {
    return name.length < 5;
});
```

3. Метод `map` - берет массив и позволяет изменить каждый элемент внутри него. Соответственно на выходе получается новый
   массив.

```JavaScript
const answers = ['IvAn', 'AnnA', 'Hello'];

const result
answers.map(item => item.toLowerCase());
```

4. Метод `some` - перебирает массив, и если хотя бы один элемент подходит под условие, заданное в функции, то
   вернет `true`, иначе `false`.

```JavaScript
const some = [4, 'qwe', 'dsvfsbvfd'];

some.some(item => typeof (item) === 'number');
```

5. Метод `every` - перебирает массив, и все элементы подходят под условие, заданное в функции, то вернет `true`,
   иначе `false`.

```JavaScript
const some = [4, 'qwe', 'dsvfsbvfd'];

some.every(item => typeof (item) === 'number');
```

6. Метод `reduce` - служит для схлопывания массива, или для сбора массива в одно единое целое.

```JavaScript
const arr = [4, 5, 1, 3, 2, 6];

//получить сумму всех элементов массива
const res = arr.reduce((summ, current) => sum + current);

//сложение всех строк в одну
const arr = ['apple', 'pear', 'plum'];

const res = arr.reduce((sum, current) => `${sum}, ${current}`);
```

Пример использования этих методов на практике:

```JavaScript
const obj = {
    ivan: 'person',
    ann: 'person',
    dog: 'animal',
    cat: 'animal'
};

const newArr = Object.entries(obj)
    .filter(item => item[1] === 'person')
    .map(item => item[0]);
```

## 4.7 npm проект. json-server

Создание npm проекта:

1. проинициализировать npm проект `npm init` -> ряд вопросов
    - package name: задать имя если не устраивает по умолчанию
    - version:
    - description:
    - entry point:  главный файл
    - test command:
    - git repository: можем сразу указать url нашего репозитория
    - keywords: ключевые слова по которым мы описываем наш проект
    - author:
    - license:
    - все
2. Появляется файл с настройками `package.json`

3. Установка json-servera [json-server](https://github.com/typicode/json-server)
    - `npm i json-server --save-dev`
4. Появляется файл package-lock.json и папка node-modules со всемя пакетами **!!НЕ ИЗМЕНЯТЬ ЕЕ И НИЧЕГО С НЕЙ НЕ
   ДЕЛАТЬ!!**
5. Установка пакетов проекта, скачанного с репозотория, когда есть только файл package.json:
    - устанавливается командой `npm i`

6. файл package-lock.json:
    - не трогаем - записаны мини зависимости проекта

7. Запуск json-server:
    - скопировать файл с базой данных (db.json)
    - задать команду `npx json-server db.json` - где db.json - это путь к файлу с данными
    - заустить json-server в gulp [Doc](https://github.com/GrafGenerator/gulp-json-server/blob/master/SAMPLES.md)

## 4.8 Получение данных с сервера. Async/Await

Заполнение карточек сейчас сделано в ручную в скрипте, но можно их заполнение сделать динамически и внешнего файла (
db.json) или из базы данных. Можно менять данные через административные панели (админки).

## 4.9 Библиотека Axios

[Documentation](https://github.com/axios/axios)

## 4.10 Сохранение данных без БД. Работа с localStorage

localStorage - технология, позволяющая сохранять данные без сервера и базы данных. Это объект, который встроен в
браузер. Размер около 5 Mb

```JavaScript

localStorage.setItem('number', 5); //сохраняет ('ключ', значение) в localStorage
localStorage.getItem('number'); // получает значение по ключу из localStorage
localStorage.removeItem('number');// удаление значения по ключу из localStorage
localStorage.clear(); //очистка хранилища
```

Работа с localStorage:

- Мы хотим, чтобы сохранилось состояние (галочка в checkbox, цвет кнопки) элементов на странице даже после обновления страницы, мы сохраняем их состояние в localStorage

```JavaScript
const checkbox = document.querySelector('#checkbox'),
        form = document.querySelector('form'),
        change = document.querySelector('#color');

if (localStorage.getItem('isChecked')) {
    checkbox.checked = true;
}

if (localStorage.getItem('bg') === 'changed') {
   form.style.backgroundColor = 'red';
}

checkbox.addEventListener('change', () => {
    localStorage.setItem('isChecked', true);
});

change.addEventListener('click', () => {
   if (localStorage.getItem('bg') === 'changed') {
       localStorage.removeItem('bg');
       form.style.backgroundColor = '#fff';
   } else {
       localStorage.setItem('bg', 'changed');
       form.style.backgroundColor = 'red';
   }
});
```

В localStorage мы можем записать свои объекты и массивы, только нужно сделать сериализация.

```JavaScript
const person = {
    name: 'Alex',
   age: 25
};

const serializedPerson = JSON.stringify(person);
localStorage.setItem('alex', serializedPerson);
```

## 4.11 Геттеры и сеттеры

```javascript
const person = {
    name: 'Alex',
    age: 25,
   
   get userAge() {
        return this.age;
   },
   set userAge(num) {
        this.age = num;
   }
};
```

## 4.12 Инкапсуляция

```javascript
function User(name, age) {
    this.name = name;
    let userAge = age;
    
    this.say = function () {
        console.log(`User name ${this.name}, age ${userAge}`);
    }
}
```

## 4.13 Webpack

1. [CommonJS](https://largescalejs.ru/commonjs-modules/)

```javascript
// First file 1.js
function myModul() {
    this.hello = function () {
        console.log('hello');
    };
    this.goodby = function () {
        console.log('bye!');
    };    
}
//Export to another file
module.exports = myModul;

//Second file 2.js
const myModule = require('./main');

const myMOduleInstance = new myModule();
myMOduleInstance.hello();
myMOduleInstance.goodby();
```

[Webpack](https://webpack.js.org/guides/getting-started/)

## 4.14 Babel

[Babel documentation](https://babeljs.io/docs)

1. Установить Babel как npm пакет: (см. документацию)
2. Настроить Babel. Настраивается в настройках Webpack или в настройках gulp

```javascript
module: { // свойства модулей, какие будем использовать
    rules: [ // правила, которые будудт действовать для определенных файлов
         {
             test: /\.m?js$/,  // находим js-ные файла с любым названием
             exclude: /(node_modules|bower_components)/, // какие файлы и папки мы должны исключить из этой выборки
             use: { // описывается как и что мы будем использовать
                 loader: "babel-loader", // используем этот loader, он является технологией, которая связывает Webpack и Babel, для того чтобы он работал, его нужно установить 
                 options: { // опции, которые будут здесь использоваться
                     presets: [ // пресеты
                         [
                             "@babel/preset-env",
                             {
                                 debug: true, // позволяет увидеть все что происходит во время компиляции
                                 corejs: 3, // библиотека с полифилами
                                 useBuiltIns: "usage", // функция, которая прикрепляет только те полифилы, которые нужны 
                             },
                         ],
                     ],
                 },
             },
         },
     ],
 },
```

3. Необходимо в файле **package.json** добавить список браузеров [BrowserList](https://browserslist.dev/?q=bGFzdCAyIHZlcnNpb25z)

```json
 "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
```

## 4.15 Библиотеки и фреймворки

1. Фреймворк **Angular** что нужно знать, чтобы на нем работать:
   - Node.js - хотя бы установить
   - TypeScript - очень похожий на js
   - Webpack
   - MVC pattern - шаблон проектирования
   - Angular [Documentation](https://angular.io/)
2. Библиотека **React** что нужно знать, чтобы на нем работать:
   - Node.js - хотя бы установить
   - Препроцессор JSX
   - Babel
   - Webpack
   - React [Documentation](https://ru.legacy.reactjs.org/)
3. Фреймворк **Vue.js** что нужно знать, чтобы на нем работать:
   - Node.js - хотя бы установить
   - Native JavaScript
   - Webpack
   - Vue.js

## 4.16 Библиотека jQuery

[Documentation](https://jquery.page2page.ru/index.php5/%D0%97%D0%B0%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%B0%D1%8F_%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0)

1. Чтобы начать работать с jQuery, надо сначала его установить. `npm i jquery --save`
2. Обновить Webpack `npm install webpack@latest`
3. Чтобы запустить в gulp нужно:
   - актуализировать **gulpfile.js**
   - установить необходимые пакеты ("gulp", "browser-sync", "webpack-stream")
   - запустить gulp

Примеры работы с jQuery
вместо функции window.addEventListener('DOMContentLoaded', () => {});
главная функция, внутри которой все бежит

```javascript
$(document).ready(() => {
   $('.list-item:first').hover(function () {
      $(this).toggleClass('active');
   });

   $('.list-item:eq(2)').on('click', () => {
      $('.image:even').fadeToggle();
   });

   $('.list-item:eq(4)').on('click', () => {
      $('.image:odd').animate({
         opacity: 'toggle',
         height: 'toggle'
      }, 2000);
   });
});
```

## Какие проекты можно придумать и реализовать самостоятельно
Довольно часто у новичков возникает вопрос: а какие дополнительные проекты можно реализовать в свое портфолио или просто для практики? Постараюсь немного помочь с этим. Заметка относится и к части про React. Все это можно сделать как на нативном JS, так и с использованием любых библиотек.

Начну с самого простого и очевидного. В реальной работе мы с вами будем получать макеты, верстать их и потом оживлять при помощи разных видов JS. Так почему бы не сделать точно так же сейчас? Вы сразу будете готовиться к реальной работе. Хороший пример этому - последний модуль в данном курсе.

Но можно и на просторах интернета и в телеграм каналах находить макеты. Потом изменять их содержимое так, чтобы они выглядели реально живыми проектами: текста, картинки, цвета и тп. Потом их верстать, так как это неотъемлемая часть фронтенда. И уже приступать к практике на JS. Можно и дополнительных функциональностей понапридумывать в проект.

Так вы точно столкнетесь со всеми реальными проблемами в работе. Научитесь их решать, набьете шишек и получите проект в портфолио.

А дальше могу предложить вам идеи для реализации. Все тоже самое, но интерфейс будет строится вокруг задачи, вокруг определенного сервиса. И придется еще придумать свой дизайн 🙂

1. Приложение-викторина.
Задача проста: на странице будут показываться вопросы с вариантами ответов. Пользователь отвечает, а в конце будет выведен результат. Хороший пример - это предыдущий практический тест) Можно реализовывать как в связке с сервером, так и без.
Я вам даже больше скажу, на фрилансе попадаются такие заказы (постил даже в тг-канал такие). Ведь кто-то делает же такие интерфейсы.

2. Видео или аудиоплеер. 2019 году косвенно участвовал в разработке очень большого проекта, где как-раз разрабатывали свой плеер. Он брал видео с серверов Амазона (предварительно залитые) и воспроизводил на фронте. Так что не думайте, что это ненужная практика 🙂

3. Приложение-библиотека.
С функционалом хранения книг из категорий: прочитано, читаю, в планах. Фильтрами по жанрам, оценкам и тп. Возможностью создавать свои подборки или списки.

4. Приложение с карточками для изучения иностранных слов.
По функционалу:
показывать слово и при клике на кнопку перевод;
случайный порядок карточек;
помню/не помню;
статистика запоминаний, анимации и тп. Можно ориентироваться на реально существующие приложения для тех же мобильных телефонов.

5. Игры: тетрис, гонки, виселица и тд. Хорошая практика с множеством концепций, но на любителя)

6. Онлайн-чат. Тоже встречается как тестовое задание, поэтому лишним не будет.
Можно добавить и функцию шифрования сообщений каким-либо способом.

7. Приложение для определения скорости печати. Очень крутая практика. Можно расширить функционал и сделать разного рода тесты. Например, за сколько вы напечатаете первый абзац n-книги и сколько ошибок допустите, с выводом нужно текста на экран + напечатанный текст

8. Генератор рандомных паролей с указание степени сложности

9. Любое приложение на базе готового API. Дальше по курсу мы будем учиться как работать с открытыми источниками данных и там я покажу массу крутых, уже готовых инструментов. Их можно взять за основу, но более наглядно я покажу дальше.

10. Взять идею из реальной жизни:
- список продуктов в холодильнике + что нужно купить
- план техосмотра вашей машины с датами, тратами и тп
- план поездки во время отпуска, со всеми тратами, остановками, возможностью все это редактировать.

Главное - это показать работодателю, что вы умеете справляться с реальными проблемами, ведь все перечисленное выше может быть реально заказано в виде веб-продукта. Именно в этом и суть такой практики. Удачи 🙂 
