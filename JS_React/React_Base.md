# 5. Библиотека React. Базовый уровень

[5.1 Элементы и компоненты](#51-элементы-и-компоненты)<br/>
[5.2 Свойства компонентов (props)](#52-свойства-компонентов-props)<br/>
[5.3 Работа со списками и алгоритм согласования](#53-работа-со-списками-и-алгоритм-согласования)<br/>
[5.4 Состояние компонентов](#54-состояние-компонентов)<br/>
[5.5 События в React](#55-события-в-react)<br/>
[5.5.1 Применение на практике](#551-применение-на-практике)<br/>
[5.6 Работа с формами, управляемые и неуправляемые компоненты](#56-работа-с-формами-управляемые-и-неуправляемые-компоненты)<br/>
[5.7 Иммутабельность объектов и собственные события ](#57-иммутабельность-объектов-и-собственные-события)<br/>
[5.8 Подъем состояния (state lifting)](#58-подъем-состояния-state-lifting)<br/>
[5.9 React фрагменты](#59-react-фрагменты)<br/>
[5.10 Styled components](#510-styled-components)<br/>
[5.11 Styles in React](#511-styles-in-react)<br/>

## 5.1 Элементы и компоненты

Компоненты - это блоки пользовательского интерфейса, которые могут иметь собственное поведение. Компоненты пишутся с большой буквы. Это какая-то функция (классическая или стрелочная), которая возвращает JSX элементы, которые должны быть заключены в круглые скобки.

Пример:
```javascript
const Element = () => {
    return ( //возврат элемента оюязательно в круглых скобках
        <div> <!--Обязательно должен быть родительский блок-->
            <h2 className="text">Tekst: {text}</h2>
            <input type="text"/>
            <label htmlFor=""></label>
            <button tabIndex="0">Click</button>
        </div>
    );
}
```
Элементы - это структурные частички компонентов. Они неизменяемые. Они могут быть заново пересозданы и потом помещены на страницу.

## 5.2 Свойства компонентов (props)

Рrops - это свойства компонента. Передаются как аргументы функции компонента. В случае, если пропсы - объект или массив, то аргументом будет деструктурированный объект или объект формата `{...props}`, которая раскладывает массив на отдельные элементы.
```javascript
function WhoAmI({name, surname, link}) {
    return (
      <div>
          <h1>My name is {name}, surname - {surname}</h1>
          <a href={link}>My profile</a>
      </div>
    );
}
function App() {
  return (
    <div className="App">
        <WhoAmI name="John" surname="Doe" link="facebook.com"/>
        <WhoAmI name="Alex" surname="Smith" link="insta.com"/>
    </div>
  );
}
```

Компонент не **ДОЛЖЕН** изменять свои пропсы. Чтобы его изменить, нужно целый компонент отрендерить заново. Как пропсы можно передавать объекты, функции.

## 5.3 Работа со списками и алгоритм согласования

1. Алгоритм согласования:
   При динамическом изменении элемента (изменении прорпсов), реакт проходит по всем элементам и сравнивает их и если он видит, что старый элемент отличается от нового, то он берет и вставляет новый элемент вместо старого. Внутри пропсов есть уникальный элемент **key**, который указывает если элемент менялся или нет (наподобие hash объекта в Java). Данные ключи должны быть уникальны среди своих соседей, но не глобально. Иногда случается, что с БЕ приходят данные без уникального идентификатора. В таком случае можно сделать индекс элемента i:
```javascript
const elements = data.map((item, i) => {
    const {id, ...itemProps} = item;
    return (
        <EmployeesListItem key={i} {...itemProps}/>
    );
});
```
, но делается это в крайнем случае, если заранее известно, что порядок элементов меняться не будет. Также считается плохой практикой назначение key через Math.random(). Этот алгоритм нужен для оптимизации скорости работы.  

**Выводы:**
1. Реакт в интерфейсе обновляет только те элементы, которые реально изменились.
2. В этом ему помогает алгоритм согласования, который сравнивает старые и новые копии DOM-дерева.
3. При работе со списком одинаковых сущностей использовать аттрибут **key** для правильной работы алгоритма и ускорения работы приложения.

## 5.4 Состояние компонентов

Динамическая "вещь" внутри компонента - это состояние компонента (state).
1. Состояние классовых компонентов.
```javascript
nextYear = () => {
        this.setState(state => ({
            years: state.years + 1
        }))
    }
```

Метод **setState()** запускает перерисовку компонента, а именно вызывает метод render().

**Выводы:**
1. У компонента может какое-то внутренне состояние, которое динамически меняется
2. Оно может быть как у классовых так и у функциональных компонентов
3. **state** напрямую менять нельзя, только через команду **setState()**
4. изменение **state** - это асинхронная операция, так что если нам нужна последовательность данных, то мы должны передавать **callback**
5. В команде **setState()** мы можем менять только те состояния, которые нам нужны. Остальные останутся без изменений.

## 5.5 События в React

```javascript
class WhoAmI extends Component {
   constructor(props) {
      super(props);
      this.state = {
         years: 27,
         position: ''
      }
      this.nextYear = this.nextYear.bind(this);
   }

   nextYear = () => {
      console.log('+++');
      this.setState({
         years: this.state.years + 1
      })
   }

   commitInputChanges = (e) => {
      this.setState({
         position: e.target.value
      })
   }

   render() {
      const {name, surname, link} = this.props;
      const {position, years} = this.state;
      return (
              <div>
                 <button onClick={this.nextYear}>+++</button>
                 <h1>My name is {name}, surname - {surname},
                    age - {years},
                    position - {position}
                 </h1>
                 <a href={link}>My profile</a>
                 <form>
                    <span>Enter </span>
                    <input type="text" onChange={this.commitInputChanges}/>
                 </form>
              </div>
      )
   }
}
```

## 5.5.1 Применение на практике

```javascript
onIncrease = () => { // как обычно вся конструкция - это callback, который принимает в себя один аргумент - state, чтобы не писать state.increase очень частоберут и деструктуризируют его прямо в аргументах ({increase})
        this.setState(({increase}) => ({ // далее ставятся круглые скобки, чтобы не прописывать return и мы просто возвращвем объект из setState
            increase: !increase // внутри объекта мы устанавливаем новое свойство increase, которое будет противоположным тому, что было до этого и из-за того что у нас стоит callback, мы будем четко отталкиваться от предидущего результата
        }))
    }
```

## 5.6 Работа с формами, управляемые и неуправляемые компоненты

```javascript
onValueChange = (e) => {
        this.setState({
           //[e.target.name] так в квадратных скобках ьы можем записать свойство в объект
            [e.target.name] : e.target.value
        })
    }
```

```javascript
<EmployeesListItem
        key={id}
        {...itemProps}
        onDelete={() => onDelete(id)} // прием называется передача property, т.е. передача свойств по иерархии от самого верхнего самому нижнему (property dril)
/>
```

## 5.7 Иммутабельность объектов и собственные события

Одно из свойств **setState** - нельзя изменять состояние объектов state, это противоречит принципу Реакт, поскольку state иммутабельны. 

1. Пример изменения state (длинный), не очень удобный:

```javascript
deleteItem = (id) => {
        this.setState(({data}) => {
            const index = data.findIndex(element => element.id === id);
            const before = data.slice(0, index);
            const after = data.slice(index + 1);

            const newData = [...before, ...after];
            return {
                data: newData
            }
        })
    }
```
2. Пример изменения state:

```javascript
deleteItem = (id) => {
        this.setState(({data}) => {
           return {
              data: data.filter(item => item.id !== id)
           }
        })
    }
```

## 5.8 Подъем состояния (state lifting)

Прием, когда внутреннее состояние одного компонента поднимаем выше по иерархии, называется подъемом состояния или state lifting. Это очень важно делать, когда у нас все данные хранятся на самом верхнем уровне. Компонент, который контролирует контролирует все приложение, называется источником истины. Именно в таком варианте нужно уметь пробрасывать данные как вниз, так и наверх.

1-й вариант:

```javascript
onToggleIncrease = (id) => {
        this.setState(({data}) => {
            const index = data.findIndex(elem => elem.id === id);

            const old = data[index];
            
           // разворачивание объекта для получения всех его свойств, результат новый объект
            const newItem = {...old, increase: !old.increase};
           // причем записанные после свойства берутся и заменяются в развернутом объекте
           
            const newArr = [...data.slice(0, index), newItem, ...data.slice(index + 1)];

            return {
                data: newArr
            }
        })
    }
```

2-й вариант:

```javascript
onToggleIncrease = (id) => {
    
    //поскольку мы не можем изменять объект state напрямую 
   this.setState(({data}) => ({
      
      // поэтому здесь мы вызвращаем новый объект, у кторого будет свойство data:
      // здесь будет формироваться новый массив (map возвращает новый массив) 
      // причем через callback функцию, которая находится внутри
      data: data.map(item => {
          
          // происходит перебор всех объектов массива data
         if (item.id === id) {
             
             // если у нас совпали id, то значит мы нашли нужный нам объект
            // в этом случае мы возвращаем новый объект, который содержит 
            // старые свойства + свойство increase, которое поменял свое значение на противоположное
            return {...item, increase: !item.increase}
         }
         // если условие не выполнилось, то мы возвращаем возвращаем этот объект
         // и как итого мы получим массив объектов только с одним новым измененным значением
         return item;
      })
   }))
}
```

## 5.9 React фрагменты

При создании компонента всегда создается один пустой \<div>. В реальной верстке он иногда может все ломать. Иногда от него нужно избавляться. Для этого в React существуют фрагменты.

## 5.10 Styled components

Компоненты, которые можно стилизовать прямо в js коде. Для того чтобы начать использовать, этот пакет необходимо установить командой `npm i --ssve-dev styled-components`.

```javascript
const Wrapper = styled.div`
  width: 600px;
  margin: 80px auto 0 auto;
`
```

Доннее компоненты можно экспортировать в другие модули, использовать там, и даже, используя наследование, переназначить стили.

```javascript
import {Button} from "./App";
import styled from "styled-components";

const BigButton = styled(Button)`
  margin: 0 auto;
  width: 245px;
`
```

Если мы хотим переопределить один компонент, скажем из тэга **\<div>** в тег **\<a>**, нужно сделать следующее: `<BigButton as="a">Send report</BigButton>`, т.е. используем тэг **\<div>** как тег **\<a>**.

Styled components поддерживают вложенность стилей, например как препроцессоры SASS/SCSS. 

```javascript
const EmpItem = styled.div`
  padding: 20px;
  margin-bottom: 15px;
  border-radius: 5px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, .2);
  a {
    display: block;
    margin: 10px 0 10px 0;
    color: black;
  }
  input {
    display: block;
    margin-top: 10px;
  }
`;
```

Также стили можно динамически менять: `color: ${props => props.active ? 'orange' : 'black'};`

1. Вендорные префиксы прописываются автоматически
2. Различные отношения CSS селекторов будут спокойно работать
3. Псевдо элеменгты и псевдо-селекторы точно также работают
4. Моно создавать анимации точно также

Главный профит - МЫ ИЗБАВИЛИСЬ ОТ CSS КЛАССОВ

Плюсы:
1. Инкапсуляция стилей - все изолированы друг от друга и нет никаких пересечений
2. Нет необходимости использовать методики типа БЭМ
3. Использование пропсов и условий
4. Браузерные (вендорные префиксы) ставятся автоматически

Минусы:
1. Нужно ко всему этому привыкнуть
2. Если подряд прописываем несколько стилизованных коапонентов, то можно запутаться где, какой тэг находится
3. Некоторые компоненты в определенных случаях можно реализовать стилями
4. Название стилей превращаются в кашу (некие рандомно сгенерированные подобия), что усложняет работу с консолью разработчика (DevTools) в браузере
5. Если CSS и JS вместе, то они вместе до конца, отдельно закэшировать нельзя
6. Если разработчик где-то ошибся, то все приложение рухнет: если опечататься в стилях, то они просто не применятся. Если опечататься в названии тэга, то приложение падает.

## 5.11 Styles in React

1. [React-Bootstrap](https://react-bootstrap.github.io/)
2. [Reactstrap](https://reactstrap.github.io/?path=/story/home-installation--page)
3. [Material Design](https://mui.com/)
4. [CSS Modules](https://habr.com/ru/articles/335244/)
5. [Ant design](https://ant.design/)

React Bootstrap - для его использования нужно сначала установить `npm install react-bootstrap bootstrap --save`, потом необходимо импортировать все стили в главный файл приложения `import 'bootstrap/dist/css/bootstrap.min.css';`