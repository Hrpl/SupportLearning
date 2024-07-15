# React 

Для создания приложение React необходимо выполнить команду
```cmd
npm create vite@latest
npm install
npm run dev
```

## Структура React приложения 
Основой React является файл index.html в котором рендерится корневой элемент main.jsx  
Что бы создать компонент, надо создать функции, где в return() будут прописан html код и экспортировать эту функцию.


## Синтаксис
Для импорта картинок
```jsx
import logo from './logo.svg'
<img src={logo} />
```

Для передачи параметров
```jsx
export default function Way({props}){
  <p>{props.title}</p>
}

function App(){
  return(
    <Way title="Заголовок"/>
  )
}
```
Т.е. мы можем обращаться к различным атрибутам элемента, которые будут хранится в объекте props. Либо же можем использовать одноимённые параметры.  
Так же возможен другой способ
```jsx
export default function Way({children}){
  <p>{children}</p>
}

function App(){
  return(
    <Way>Заголовок</Way>
  )
}
```
Всё, что будет между тегами, будет поподать в children  

Для отслеживания событий в дочернем компоненте

```jsx
export default function Button({eventClicked}){
  <button  onClick={eventClicked}></button>
}


export default function App(){

  function handleClick(type){
    console.log(type)
  }

  return(
  <Button onClick={() => handleClick('param')}>
  )
}
```

Для определения классов можно использовать следующий синтаксис. Важно то, что инлайе стили необходимо передавать как объекты js, а не строки.
```jsx
if(isActive === 'active') isActive = true

<button className={isActive ? 'btn active' : 'btn'}></button>
```
Все компоненты React содержать возращаемое значение с кодом - оно обязательно должно быть одинарным, либо передаваться как массив. Это объясняется тем, как работает jsx и имеет следующий синтаксис

```jsx
import React from 'react'
export default function App(){
  return React.createElement('div', null, [
    return React.createElement('p', 
      {className: {'flex', style: {color: 'red'}}}, 
      "Содержание тега"
    )
  ])
}
```

Привязка данных к форме осуществляется следующим образом Two Way Binding
```jsx
import {useState} from 'react'

export default function App(){
const [content, setContent] = useState('')

return(
  <input value={content} onChange="(event) => setContent(event.target.value)">
)
}
```
## Реактивность и отслеживания состояния

Для отслеживания состояний необходимо импортировать следующий хук
```jsx
import {useState} from 'react'

export default functiom App(){
  const [value, setValue] = useState(1)

  return(
  <button onClick={() => setValue(value++)}></button>
  //остальной код)
}
```
Для отслеживания состояний нескольких переменных можно их значения хранить в объекте, для этого возможен следующий синтаксис
```jsx
import {useState} from 'react'

export default functiom App(){
  const [form, setFrom] = useState({
    name: '',
    female: '',
    surname: ''
  })

  return(
  <input value={form.name} onChange={(event) => setForm((prev) => {...prev, name: event.target.value})}>
  //остальной код)
}
```
Хук useState определяет объект со всеми полями, а input обновляет значение только поля name. Что бы не потерять все значения, используется спред оператор(...prev), который раскладывает объект на оставшиеся поля

**useEffect()***, он принимате два параметра: первый - callback, второй - массив реактивных параметров, при изменении которых, будет выполняться callback. При пустых массиве, функция будет вызываться только один раз при монтировании элемента. Так же в этом хуке обрабатываются все запросы к серверу.  
При размонтировании компонента будет выполняться часть кода в return().

***useReef()*** используется для того чтобы создать ссылку на html элемент и с помощью .current управлять его атрибутами ( как пример - задать некоторые стили для этого элемента)
```jsx
const textRef = useRef(null)

  const onClick = () => {
    textRef.current.style.color = 'red'
  }
  
  return (
    <>
    <span ref={textRef}>Красный цвет текста</span>
    <button  className=""  onClick={onClick}> Нажми</button>
    
    </>
  )

```
***useCallback*** - кэширует функцию Callback, используем когда передаем Callback дочерним компонентам или хотим избежать ненужных рендеров.  
***useMemo*** - кэшируте результат функции и используется для оптимизации производительности за счёт сохранения точных вычислений.  
