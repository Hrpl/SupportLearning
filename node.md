В Node существуют глобальные объекты, которые осуществляют доступ к чему-либо, полный список можно просмотреть в документации  
Основа node.js - работа с модулями  

``` js
const http = require('http');

const fs = require('fs'); // модуль файловой системы, к примеру для передачи html страниц
const path = require('path'); // формирование путей

const server = http.createServer((req, res) => { // создание сервера
    console.log("request");

    res.setHeader('Content-Type', 'text/html') // возращает заголовки в виде html
    res.write('<h1>Hello word!</h1>'); // запись ответа клиенту


    res.setHeader('Content-Type', 'application/json') // настройка заголовка для передачи JSON

    const data = JSON.stringify([ // возврат JSON
        {name: 'Tom', age: 28}
    ])

    res.end(data); // передача запроса обратну клиенту
})

server.listen(3000, 'localhost', (error) =>{ // создание прослушки на порту 3000
    error ? console.log(error) : console.log('listening port 3000');
})
```
