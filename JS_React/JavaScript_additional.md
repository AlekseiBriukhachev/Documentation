# 2. Дополнительные основы JavaScript

## Содержание

[3.1 Nullish оператор](#31-nullish-оператор)<br>
[3.2 Оператор опциональной цепочки](#32-оператор-опциональной-цепочки)<br>
[3.3 Живые коллекции и полезные функции](#33-живые-коллекции-и-полезные-функции)<br>
[3.4 Тип данных Symbol](#34-тип-данных-symbol)<br>
[3.5 Дескрипторы свойств и полезные методы объектов](#35-дескрипторы-свойств-и-полезные-методы-объектов)<br>
[3.6 Итерируемые конструкции](#36-итерируемые-конструкции)<br>
[3.7 Map](#37-map)<br>
[3.8 Set](#38-set)<br>
[3.9 BigInt](#39-bigint)<br>

### 3.1 Nullish оператор

Nullish оператор **??** - ставится за переменной у за ним указывается дефолтное значение, которое возмется в качестве значения переменной, если значение переменной ***null*** или ***undefined***

```JavaScript
console.log(username ?? 'User');
```

### 3.2 Оператор опциональной цепочки

Оператор опциональной цепочки **?.** - проверяет если значение переменной не равно ***null*** или ***undefined***

```JavaScript
const block = document.querySelector('.block');
//проверяется если значение переменной block не равно null или undefined
console.log(block?.textContent);

//используется вместо проверки
if (block) {
    console.log(block.textContent);
}
```

Данный оператор работает только на чтение переменной.

Пример использования для проверки полей объекта:

```JavaScript
const userData = {
    name: 'Ivan',
    age: null,
    say: function () {
        console.log('Hello');
    }
}

//проверка без использования оператора
if (userData && userData.skills && userData.skills.js) {
    console.log(userData.skills.js);
}

//проверка с исползованием оператора
console.log(userData?.skills?.js);

userData.say();
userData.hey?.();
```

### 3.3 Живые коллекции и полезные функции

```JavaScript
const boxesQuery = document.querySelectorAll('.box');
const boxesGet = document.getElementsByClassName('box');

boxesQuery.forEach(box => {
    if (box.matches('.this')) console.log(box);
});

console.log(boxesQuery[0].closest('.wrapper'));

boxesQuery[0].remove();
boxesGet[0].remove();

for (let i = 0; i < 5; i++) {
    const div = document.createElement('div');
    div.classList.add('box');

    // Correct
    document.body.append(div);

    // Mistake
    boxesGet[boxesGet.length] = div;
}

console.log(boxesQuery);
console.log(boxesGet);
console.log(document.body.children);

console.log(Array.from(boxesGet));
```

### 3.4 Тип данных Symbol

В ES6 введен новый тип данных **Symbol**. Применяется к свойствам объектов.

```JavaScript
const obj = {
    'name': 'Test',
    [Symbol("id")]: 1,
    getId: function() {
        return this[id];
    }
}

let id = Symbol("id");
let id2 = Symbol("id");
// символы всегда уникальны

console.log(id == id2);
obj[id] =1;

console.log(obj);
console.log(obj.getId());
console.log(obj[Object.getOwnPropertySymbols(obj)[0]]);

for (let value in obj) console.log(value);

const myAwesomeDB = {
    movies: [],
    actors: [],
    [Symbol("id")]: 123
}

//Some code

myAwesomeDB.id = '3223343232';
console.log(myAwesomeDB["id"]);
console.log(myAwesomeDB);
```

### 3.5 Дескрипторы свойств и полезные методы объектов

Флаги объекта:

- writable     ->  если флаг true, то свойства в объекте можно изменить. Если нет, то свойства только для чтения

- enumerable   ->  если флаг true, свойство будет перечисляться в циклах. Если нет, то циклы будут его игнорировать

- configurable ->  если флаг true, то свойство можно удалить, а аттрибуты можно изменить. Если нет, то делать этого нельзя

```JavaScript
    const user = {
        name: 'Alex',
        surname: 'Smith',
        // birthday: '20/04/1993',
        showMyPublicData: () => {
            console.log(`${this.name} ${this.surname}`);
        }
    }
```

1. ПРИМЕР 1 - С ПРИМЕНЕНИЕМ ФЛАГА **WRITABLE**

```JavaScript
    Object.defineProperty(user, 'birthday', {
        value: prompt('Date?'), 
        enumerable: true,
        configurable: true
    });

    console.log(Object.getOwnPropertyDescriptor(user, 'birthday'));
    console.log(Object.getOwnPropertyDescriptor(Math, 'PI'));

    Object.defineProperty(user, 'name', {writable: false});
    //ОШИБКА!
    user.name = 'kjhscsac';
    Object.defineProperty(user, 'gender', {value: 'male'});
    console.log(Object.getOwnPropertyDescriptor(user, 'gender'));
    //у этого созданного свойства все флаги установлены дефолт в false
```

2. ПРИМЕР 2 - С ПРИМЕНЕНИЕМ ФЛАГА **ENUMERABLE**

```JavaScript
    Object.defineProperty(user, 'showMyPublicData', {enumerable: false});

    for (let key in user) console.log(key);
```

3. ПРИМЕР 3 - С ПРИМЕНЕНИЕМ ФЛАГА **CONFIGURABLE**

Дорога в один конец - после установки этого флага, объект перестает реагировать на Object.defineProperty()

4. Изменение сразу несколько свойств

```JavaScript

    Object.defineProperties(user, {
        name: {writable: false},
        surname: {writable: false}
    });
```

ПОЛЕЗНЫЕ МЕТОДЫ

|Метод|Описание|
|-:|:-|
|Object.preventExtensions()|предотвращает любое расширение объектов, блокирует добавление данных в объект|
|Object.seal()|"запечатывает" объект, предотвращает добавление новых свойств к объекту и делает все существующие свойства ненастраиваемые|
|Object.freeze()|замораживает объект, запрещает какие-либо изменения объекта|
|Object.is()|сравнивает два объектапо значению|
|[Object.keys()](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)|возвращает массив (ключей) из собственных перечисляемых свойств переданного объекта|
|[Object.values()](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/values)|возвращает массив значений перечисляемых свойств объекта|
|[Object.entries()](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)|возращает массив собственных перечисляемых свойств объекта в формате (ключ, значение)|

### 3.6 Итерируемые конструкции

Отличия for-of от for-in ([for..in versus for..of Loops](https://bitsofco.de/for-in-vs-for-of/))

```JavaScript
const user = {
    name: 'Alex',
    surname: 'Smith',
    birthday: '20/04/1993',
    showMyPublicData: () => {
        console.log(`${this.name} ${this.surname}`);
    }
}
```

for-in при использовании на объекте, массиве или строке будет работать с каждой сущностью по порядку, которая является перечисляемой, получает ключ ([for...of](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/for...of))

```JavaScript
for (const key in user) {
    console.log(user[key]);
}

const arr = ['b', 'a', 'c'];
for (const key in arr) {
    console.log(arr[key]);
}

const str = 'string';
for (const key in str) {
    console.log(str[key]);
}
```

есть проблема - может быть такое, что перебор будет идти не по порядку - ***не рекомендуется применять на массивах и строках***

В ES6 стандарте бsл введен цикл for-of - он проходится по значениям перебираемого объекта - получает значение

```JavaScript
const arr = ['b', 'a', 'c'];
for (const key of arr) {
    console.log(key);
}
for (const key of user) {
    console.log(user[key]);
}
// возникает ошибка - объект не перебираемый
```

Перебираемый или итерируемый объект - это тот объект, который мы можем использовать в for-of, определяется тем, если у этой сущности есть символ **.iterator**

**перебираемые сущности** - массивы, строки, типизированные массивы, set, map, DOM-коллeкции

Преимущества:

1. Строгое соответствие порядка в переборе - как оно было записано в оригинале, так оно и будет выполнятся

2. Исключение всех лишних свойств, которые могут быть унаследованы.

```JavaScript
const arr = ['b', 'a', 'c'];
Array.prototype.someMethod = function() {};
console.dir(arr);
for (const key in arr) {
    console.log(key);
}
// в косоль выводится 0, 1, 2, someMethod
for (const key of arr) {
    console.log(key);
}
// в косоль выводится b, a, c отбрасывается прототипный наследванный метод
```

Как добавить символ **.iterator** к обычному объекту ([How to iterate over a JavaScript object?](https://stackoverflow.com/questions/14379274/how-to-iterate-over-a-javascript-object))

Дословно: итератор - это метод, который возвращает объект с методом **next()**, итератор приходится создавать вручную

```JavaScript
const salaries = {
    john: 500,
    ivan: 1000,
    ann: 5000,
    sayHello: () => {
        console.log('Hello');
    }
}

salaries[Symbol.iterator] = function() {
    return {
        current: this.john,
        last: this.ann,

        next() {
            if (this.current < this.last) {
                this.current += 500;
                return {done: false, value: this.current}
            } else {
                return {done: true}
            }
        }
    }
}

for (let res of salaries) {
    console.log(res);
}

// Вместо for-of можно итератор вызывать вручную:
const iterator = salaries[Symbol.iterator]();
console.log(iterator.next());
```

### 3.7 Map

Картами или map называются специфические структуры данных, которые очень похожи на объект. Только у них вместо свойств может использоваться и объект, и массив, и функция. У них есть свои методы.

```JavaScript
    const user = {
        name: 'Alex',
        surname: 'Smith',
        birthday: '20/04/1993',
        showMyPublicData: () => {
            console.log(`${this.name} ${this.surname}`);
        }
    }
```

Перевод объекта в map

```JavaScript
    const userMap = new Map(Object.entries(user));
    console.log(userMap);
```

Перевод map в объект

```JavaScript
    const newUserObj = Object.fromEntries(userMap);
    console.log(newUserObj);
```

Методы map:

```JavaScript
    const shops = [
        {rice: 500},
        {oil: 200},
        {bread: 50}
    ]


    const budget = [5000, 15000, 25000];

    const map = new Map([
        [{paper: 400}, 8000]
    ]);

    shops.forEach((shop, i) => {
        map.set(shop, budget[i]);
    })

    map.set(shops[0], 5000)
        .set(shops[1], 15000)
        .set(shops[2], 25000);

    console.log(map);
    console.log(map.get(shops[0]));
    console.log(map.has(shops[0]));

    map.get(shops[0]); //получение

    map.has(shops[0]); //если есть такой объект

    map.delete(key); //удаление

    map.clear(); // очистка целиком мапы

    map.size; //размер

    map.keys(); // получение объекта по ключам

    console.log(map.keys());
```

Способы перебора map:

1. Получение объекта по ключам

```JavaScript
    const goods = [];
    for (let shop of map.keys()) {
        // console.log(shop);
        goods.push(Object.keys(shop)[0]);
    }
    console.log(goods);
```

2. Получение объекта по значениям

```JavaScript
    for (let price of map.values()) {
        console.log(price);
    }
```

3. Entries

```JavaScript
    for (let [shop, price] of map.entries()) {
        console.log(price, shop);
    }
```

4. forEach

```JavaScript
    map.forEach((value, key, map) => {
        console.log(key, value);
    });
```

### 3.8 Set

Особый вид коллекций по типу массива, где каждое значение может повторятся только один раз

```JavaScript
    // const arr = [1, 1, 2, 2, 4, 5, 6, 5];
    const arr = ['Alex', 'Ann', 'Oleg', 'Alex'];

    const set = new Set(arr);

    set.add('Ivan')
        .add('Oleg'); //добавить элемент

    console.log(set);
```

Базовые функции

```JavaScript
    set.delete(value); //удаление
    set.has(value); // проверки если существует
    set.clear(); //полная очистка
    set.size; //размер
```

Перебор

```JavaScript
    for (let value of set) {
        console.log(value);
    }
    set.forEach((value, valueAgain, set) => {
        console.log(value, valueAgain);
    });
```

Встроенные методы

```JavaScript
    console.log(set.values());
    console.log(set.keys());
    console.log(set.entries());
```

Функция помощник, которая фильтрует любой массив

```JavaScript
    function unique(arr) {
        return Array.from(new Set(arr));
    }
    console.log(unique(arr));
```

### 3.9 BigInt

Для избежания ошибок при работе с большими числами ольшим, чем Number.MAX_SAFE_INTEGER = 9007199254740991 существует тип данных **BigInt**

1й вариант создания большого числа - добавление в конце числа буквы n

```JavaScript
const bigint = 1223894793265876432863219893324863284n;
```

2й вариант с помощью встроенной команды

```JavaScript
const sameBigInt = BigInt(1223894793265876432863219893324863284);
```

Особенности:

1. BigInt нельзя использовать с методами со встроенным объектом **Math**
2. Нельзя смешивать в операциях BigInt и обычные числа

Операторы: применяются те же операторы, что и с обычными числами, только операция деления возвращает округленное целое число
