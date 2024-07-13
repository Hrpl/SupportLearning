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
export default function Way(props){
  <p>{props.title}</p>
}

function App(){
  return(
    <Way title="Заголовок"/>
  )
}
```
Т.е. мы можем обращаться к различным атрибутам элемента, которые будут хранится в объекте props
