# Top 10 JavaScript Style Guide Best Practices I Really Love

1. Используйте === вместо ==

В JavaScript существует два разных типа операций сравния: === / !== и == / !=. 
Считается хорошим тоном всегда использовать первую пару для сравнения.
“Если два операнда одного типа и значения, то === вернет true, а !== false” 

2. Переместите скрипты вниз страницы

Основная цель этого совета — заставить страницу грузиться как можно быстрее. Когда браузер грузит скрипт он не продолжит рендеринг пока весь файл не будет загружен. Таким образом пользователю придется ждать дольше.
Если ваши JS скрипты служать для добавления функционала — например, обработки кликов кнопки то вам стоит перенести скрипты вниз поставив их перед закрывающимся тегом body. 

``` html
<p>And now you know my favorite kinds of corn. </p>  
<script type="text/javascript" src="path/to/file.js"></script>  
<script type="text/javascript" src="path/to/anotherFile.js"></script>  
</body>  
</html>
```

3. Объявляйте переменные для 'for' вне циклов

Когда выполняете долгий цикл «for» не заставляйте делать движок больше работы чем нужно.

``` js
// Плохо

for(var i = 0; i < someArray.length; i++) {  
   var container = document.getElementById('container');  
   container.innerHtml += 'my number: ' + i;  
   console.log(i);  
}  
```

``` js
// Лучше

var container = document.getElementById('container');  

for(var i = 0, len = someArray.length; i < len;  i++) {  
   container.innerHtml += 'my number: ' + i;  
   console.log(i);  
}  
```

4. Уменьшите количество глобальных переменных

«Сведением количества глобальных переменных к одному, вы значительно снижаете шансы нежелательного взаимодействия с другими приложениями, виджетами или библиотеками.» 
— Douglas Crockford

``` js
// Плохо
var name = 'Jeffrey';  
var lastName = 'Way';  
  
function doSomething() {...}  
  
console.log(name); // Jeffrey -- or window.name  
```

``` js
// Лучше

var DudeNameSpace = {  
   name : 'Jeffrey',  
   lastName : 'Way',  
   doSomething : function() {...}  
}  
console.log(DudeNameSpace.name); // Jeffrey  
```

Мы уменьшили количество глобальных переменных до одного.

5. Всегда, всегда используйте точку с запятой

Технически, большинство браузеров позволят вам не использовать их.

``` js
//  Плохо

var someItem = 'some string'  
function doSomething() {  
  return 'something'  
}  
```

Но использование подобную практики потенциально может привести к гораздо более большим и что еще хуже плохо отлавливаемым проблемам.

``` js
//Лучше

var someItem = 'some string';  
function doSomething() {  
  return 'something';  
}  
```

6.  Используйте стрелочные функции всегда, когда вам нужно сохранить лексическое значение this.

``` js
function Person(name) {
    this.name = name;
}

Person.prototype.prefixName = function (arr) {
    return arr.map(character => this.name + character);
};
```

7. Используйте const для объявления переменных; избегайте var

``` js
// плохо
var a = 1;
var b = 2;

// хорошо
const a = 1;
const b = 2;
```

8. Если вам необходимо переопределять значения, то используйте let вместо var

``` js
// плохо
var count = 1;
if (true) {
  count += 1;
}

// хорошо
let count = 1;
if (true) {
  count += 1;
}
```

9. Использовать createDocumentFragment() при добавлении элементов в DOM

``` js
//Плохо

var list = document.getElementById("list"),
    items = ["one", "two", "three", "four"],
    el;

for (var i = 0; items[i]; i++) {
  el = document.createElement("li");
  el.appendChild( document.createTextNode(items[i]) );
  list.appendChild(el); // Медленно, плохая идея
}

```

``` js
//Лучше

var list = document.getElementById("list"),
    frag = document.createDocumentFragment(),
    items = ["one", "two", "three", "four"],
    el;

for (var i = 0; items[i]; i++) {
  el = document.createElement("li");
  el.appendChild( document.createTextNode(items[i]) );
  frag.appendChild(el); // Лучше!
}

list.appendChild(frag);
```

10. Объявляйте переменные в начале файла

Это хорошая практика, чтобы поместить все объявления в начало каждого скрипта или функции.

Это даст более чистый код, обеспечит единственное место для поиска локальных переменных, уменьшит вероятность нежелательных повторных объявлений переменных

``` js
// Объявляйте в начале
var firstName, lastName, price, discount, fullPrice;

// Используйте потом
firstName = "John";
lastName = "Doe";

price = 19.90;
discount = 0.10;

fullPrice = price * 100 / discount;
```