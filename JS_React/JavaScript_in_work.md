# 3. JavaScript в работа

## Содержание

[3.1 ClassList и делегирование событий](#31-classlist-и-делегирование-событий)<br>

### 3.1 ClassList и делегирование событий

|Instruction|Description|
|-:|:-|
|btns[0].classList.length|Количество элементов|
|btns[0].classList.item(1)|Значение класса по номеру элемента|
|btns[0].classList.add('red')|Добавление класса|
|btns[0].classList.remove('blue')|Удаление класса|
|btns[0].classList.toggle('blue')|Переключение класса|
|btns[0].classList.contains('red')|Проверяет наличие класса|
|btns[0].className|Выводит в консоль список всех классов данного элемента|

```JavaScript
const btns = document.querySelectorAll('button');

if (btns[1].classList.contains('red')) {
    console.log('red')
}

btns[0].addEventListener('click', () => {
    if (!btns[1].classList.contains('red')) {
        btns[1].classList.add('red');
    } else {
        btns[1].classList.remove('red');
    }
    btns[1].classList.toggle('red');
});

console.log(btns[0].className);
```

Делегирование событий

Мы берем элемент, который является родителем, и работаем с ним - назначаем обработчик событий на родителя, а внутри мы будем проверять на что мы кликнули

```JavaScript
const wrapper = document.querySelector('.btn-block');
wrapper.addEventListener('click', (event) => {
    console.dir(event.target);
    if (event.target && event.target.tagName == 'BUTTON') {
        console.log('Hello');
    }
});

const btn = document.createElement('button');
btn.classList.add('red');
wrapper.append(btn);
```

**!!ОШИБКА ДЕЛЕГИРОВАНИЯ, ПОТОМУ ЧТО ЭТОТ ПЕРЕБОР НИЧЕГО НЕ ЗНАЕТ О НОВО СОЗДАННОЙ КНОПКЕ И РАБОТАЕТ ТОЛЬКО ПРО СУЩЕСТВУЮЩИЕ КНОПКИ!!**

```JavaScript
btns.forEach(btn => {
    btn.addEventListener('click', () => {
        console.log('Hello');
    });
});

const btn = document.createElement('button');
btn.classList.add('red');
wrapper.append(btn);
```

Еще один способ, который любят сотрудники Google - использование метода `matches()`. По-простому это какой-то элемент совпадает с чем-то.

```JavaScript
wrapper.addEventListener('click', (event) => {
    if (event.target && event.target.matches("button.red")) {
        console.log('Hello');
    }
});
```

### 3.2 Скрипты и время их выполнения. Анимация

Для запуска функции через определнное время есть функция `setTimeout()`

Анонимная функция (без аргумента)

```JavaScript
const timerId = setTimeout(function() {
    console.log('Hello');
}, 2000);
```

Функция с аргументом

```JavaScript
// const timerId = setTimeout(function(text) {
//     console.log(text);
// }, 2000, 'Hello');
```

Передача функции без обявления (только название функции)

```JavaScript
const timerId = setTimeout(logger, 2000);

function logger() {
    console.log('text');
}
```

Когда записываем `const timer = setTimeout(logger, 2000);` в таком виде, мы записываем числовой идентификатор этого таймера

Сброс определенного таймера `clearInterval(timerId);`

Функция для повторения через определенный интервал,а не один раз, есть функция `setInterval()`

```JavaScript
const btn = document.querySelector('.btn');
let timerId,
    i = 0;
btn.addEventListener('click', () => {
    // const timerId = setTimeout(logger, 2000);
    timerId = setInterval(logger, 500);

});
clearInterval(timerId);
function logger() {
    if (i === 3) {
        clearInterval(timerId);
    }
    console.log('text');
    i++;
}
```

Анимация

```JavaScript
const btn = document.querySelector('.btn');
let timerId;

function myAnimation() {
    const elem = document.querySelector('.box');
    let pos = 0;

    const id = setInterval(frame, 10);
    function frame() {
        if (pos == 300) {
            clearInterval(id);
        } else {
            pos++;
            elem.style.top = pos + 'px';
            elem.style.left = pos + 'px';
        }
    }
}

btn.addEventListener('click', myAnimation);
```

### 3.3 Сборщик мусора и утечтки памяти

[Компилятор VS интерпретатор: ключевые отличия](https://nuancesprog.ru/p/12524/)

[Сборка мусора](https://learn.javascript.ru/garbage-collection)

### 3.4 Пример кэширования пользователей

```JavaScript
//Кэшировние пользователей
let cache = new WeakMap();

//функция кэширования пользователей
function cacheUser(user) {
    if (!cache.has(user)) {
        cache.set(user, Date.now());
    }
    return cache.get(user);
}

//добавились Лена, Алекс
let lena = {name: 'Elena'};
let alex = {name: 'Alex'};

//кэширование пользователей
cacheUser(lena);
cacheUser(alex);

//Лена вышла в офлайн
lena = null;

//Проверка активных пользователей
console.log(cache.has(lena));
console.log(cache.has(alex));
```

### 3.5 Работа с датами

[Дата](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Date)

[Дата и время](https://learn.javascript.ru/date)

### 3.4 Параметры документа, окна и работа с ними

![text](img/metric-all.png)

```JavaScript
const box = document.querySelector('.box');

const width = box.clientWidth;
const heigth = box.clientHeight;
const width = box.offsetWidth;
const heigth = box.offsetHeight;
const width = box.scrollWidth;
const heigth = box.scrollHeight;

console.log(width, heigth);
```

Раскрытие содержимого окна прокрутки по нажатию на кнопку:

```JavaScript
const btn = document.querySelector('button'),
	scrollHeight = box.scrollHeight,
	boxHeigth = box.offsetHeight,
	listed = document.querySelector('.progress');
```

при нажатии на кнопку переключает видимое окно на полную высоту содержимого или обратно сворачивает

```JavaScript
btn.addEventListener('click', () => {

	if (box.offsetHeight >= scrollHeight) {
		box.style.height = boxHeigth + 'px';
	} else {
		box.style.height = scrollHeight + 'px';
	}
	const boxCoordinates = box.getBoundingClientRect();
	console.log(boxCoordinates);
});
```

Прогресс прочитанного в окне прокрутки

```JavaScript
box.addEventListener('scroll', () => {
	let scrolled = box.scrollTop;
	listed.innerHTML = Math.floor((scrolled / (scrollHeight - box.clientHeight)) * 100);
});
```

Получение координат объекта

```JavaScript
const boxCoordinates = box.getBoundingClientRect();
console.log(boxCoordinates);
```

### 3.5 Работа с модальным окном

Классы **hide** и **show** добавляем сами в css **_Animation** например

```JavaScript
	const modalTrigger = document.querySelectorAll('[data-modal]'),
		modal = document.querySelector('.modal'),
		modalCloseBtn = document.querySelector('[data-close]');

	modalTrigger.forEach(btn => {
		btn.addEventListener('click', () => {
			modal.classList.add('show');
			modal.classList.remove('hide');
			document.body.style.overflow = 'hidden';

			// DRY
			openModal();

		});
	});

	modalCloseBtn.addEventListener('click', () => {
		modal.classList.add('hide');
		modal.classList.remove('show');
		document.body.style.overflow = '';

		//DRY
		closeModal();
	});
```

Вариант с **toggle()**

```JavaScript
	modalTrigger.addEventListener('click', () => {
		modal.classList.toggle('show');
		document.body.style.overflow = 'hidden';
	});
	modalCloseBtn.addEventListener('click', () => {
		modal.classList.toggle('show');
		document.body.style.overflow = '';

	//DRY
		closeModal();
	});
```

	А можно ли сделать, чтобы модальное окно закрывалось по клику на **background** или по клику на клавишу **ESC**

```JavaScript
	modal.addEventListener('click', (event) => {
		if (event.target === modal) {
			modal.classList.add('hide');
			modal.classList.remove('show');
			document.body.style.overflow = '';

			//DRY
			closeModal();
		}
	});
```

DRY - **D**ont **R**epeat **Y**ourself - не повторять код, который есть в скриптах

```JavaScript
	function closeModal() {
		modal.classList.add('hide');
		modal.classList.remove('show');
		document.body.style.overflow = '';
	}

	function openModal() {
		modal.classList.add('show');
		modal.classList.remove('hide');
		document.body.style.overflow = 'hidden';
	}
```

[JavaScript Key Code](https://www.toptal.com/developers/keycode)
		
Реакция на клавиаши клавиатуры

```JavaScript
document.addEventListener('keydown', (event) => {
		if (event.code === 'Escape' && modal.classList.contains('show')) {
			closeModal();
		}
	});
```

### 3.6 MutationObserver, ResizeObserver, contenteditable

Залать в верстке свойство элемента `<div contenteditable="true" class="box"></div>`, и можно изменять прямо на странице.

[MutationObserver](https://developer.mozilla.org/ru/docs/Web/API/MutationObserver)

```JavaScript
const box = document.querySelector('.box');
```

Создадим сущность которая будет следить за этим элементом

```JavaScript
let observer = new MutationObserver(mutationRecord => {
	console.log(mutationRecord);
});
```

Следит за элементом, если что-то в нем меняется, то выполняй эту функцию

```JavaScript
observer.observe(box, {
	childList: true
});
observer.disconnect();
```

### 3.7 Функции конструкторы

Пример функции-конструктор - функция, с помощью которой можно создавать новые объекты (например, пользователей).

```JavaScript
function User(name, id) {
	this.name = name;
	this.id = id;
	this.human = true;
}

const ivan = new User('Ivan', 28);
const alex = new User('Alex', 20);
```

### 3.8 Контекст вызова функции. This

1. 1 метод: Вызов функции - обычная функция:  `this = window`, но если стоит `'use strict'` то будет `undefined`

```JavaScript
function showThis() {
	console.log(this); // this = window
}
```

Практическая задача, котороую дают на собеседованиях

```JavaScript
function showThis(a, b) {
	console.log(this);
	function sum() {
		console.log(this); //1й вопрос: что выведет в консоль this - Ответ: undefined контекст тот же самый и не меняется
		return this.a + this.b;//2й вопрос: будет ли работать эта комбинация, и если нет то как ее исправить Ответ: не работает - ошибка. Для исправления нужно использовать замыкание функции
		return a + b;
	}
}
```

2. 2 метод: Вызов функции - создание объекта. Если мы используем метод внутри объекта, то контекст вызова всегда будет ссылаться на этот объект. Если внутри метода объекта создана простая функция, то контекст вызова этой функции будет `undefined`.

```JavaScript
const obj = {
	a: 20,
	b:15,
	sum: function() {
		console.log(this);
	}
};
```

3. 3 метод: Вызов функции - функции конструкторы. `This` в конструкторах и классах - это новый экземпляр объекта.

```JavaScript
function User(name, id) {
	this.name = name;
	this.id = id;
	this.human = true;
}
const ivan = new User('Ivan', 28);
```

4. 4 метод: Вызов функции - ручное присвоение `this` любой функции.

```JavaScript
function sayName() {
	console.log(this);
	console.log(this.name);
}

const = user = {
	name: 'John'
};

sayName.call(user);// вызов свойств объекта, переданного параметром
sayName.apply(user);
//Эти функции делают одно и то же, разницы никакой нет, только в синтаксисе.
```

5. Иетод присвоения `bind` - он создает новую функцию, связанную с присвоением контекста.

```JavaScript
function count(num) {
	return this * num;
}
const double = cont.bind(2); //здесь передаем жестко привязанный контекст.
console.log(double(3));
consle.log(double(13)); //часто используется в React
```

Как это работает на практике:

```JavaScript
const btn = document.querySelector('button');

btn.addEventListener('click', function() {
	this.style.background = 'red';
});
```

Если в обработчике событий в качестве call-back функции использована функция, написанная в классическом варианте, то контекстом будет сам элемент, на котором произошло событие.

У стрелочной функции нет своего контекста вызова, она всегда его будет брать у своего родителя.

```JavaScript
const obj = {
	num: 5,
	sayNumber: function() {
		const say = () => {
			consle.log(this);
		};

		say();
	}
};

obj.sayNumber();
```

Пример со стрелочной функцией:

```JavaScript
const btn = document.querySelector('button');

btn.addEventListener('click', (event) => {
	this.style.background = 'red';//ОШИБКА - контекст вызова потерялся
	// Для избежания ошибки нужно добавить event.target вместо this
	event.target.style.background = 'red';
});
```

### 3.9 Классы

```JavaScript
class Rectangle {
	constructor(height, width) {
		this.height = height;
		this.width = width;
	}

	calcArea() {
		return this.height * this.width;
	}
}

const square = new Rectangle(10, 10);
const long = new Rectangle(20, 100);

console.log(square.calcArea());
console.log(long.calcArea());
```

Наследование:

```JavaScript
class ColoredRectangleWithText extends Rectangle {
	constructor(height, width, text, bgColor) {
		super(height, width);
		this.text = text;
		this.bgColor = bgColor;
	}

	showMyProps() {
		console.log(`Текст: ${this.text}, цвет: ${this.bgColor}`);
	}
}

const div = new ColoredRectangleWithText(25, 10, 'Hello World', 'red');

div.showMyProps();
console.log(div.calcArea());
```

### 3.10 Rest операторы и параметры по умолчанию

rest оператор - остаточные параметры функции, которые могут придти, а могут не придти. Этот опреатор собирает в элементв массива. Обратный оператору `spred`, который раскладывает массив на элементы.

```JavaScript
const log = function(a, b, ...rest) {
	console.log(a, b, rest);
}

log('basic', 'rest', 'operator', 'usage');
```

[Остаточные параметры (rest parameters)](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Functions/Rest_parameters)
[Параметры по умолчанию](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Functions/Default_parameters)
