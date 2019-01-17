# Javascript原型鍊
Javascript當初是受到C++以及Java啟發進而創造出**原型鍊(Prototype)**，直接以下面例子舉例。

建立一個fastfood的構造函數(constructor)，表示fastfood的原型。

```
function fastfood(name){

　　　　this.name = name;

　　}
```
對這個構造函數使用new，就會生成一个速食對象的實例。
```
var fastfooda = new fastfood('Burger');
console.log(fastfooda.name);//Burger

```
注意構造函數中的this，它就代表了新建立的實例對象。

**1.new的缺點**

用構造函數生成實例對象，有個缺點，就是無法共享属性和方法。

比如，在fastfood對象的構造函數中，設置一個實例對象的共有属性foodtype。
```
function fastfood(name){

　　　　this.name = name;
       this.foodtype = '主餐';
     
　　}
```
後續建立兩個新的fastfood對象。
```
var fastfooda = new fastfood('BaconBurger');

var fastfoodb = new fastfood('BeefBurger');
```
此時建立兩個新對象屬性是獨立的，修改任一個，不會影響另一個。
```
fastfooda.foodtype = '加點';
console.log(fastfoodb.foodtype);//主餐
```
上述例子來說，每種速食的名稱都不同，沒有關連性，可不用共享資源，但兩種速食的foodtype都為主餐，此時卻無法做到資源共享，彼此沒有關聯。

若以程式角度來思考，這樣會造成資源的浪費，明明是同樣類型，卻佔據兩個空間。

如果我們想讓兩個速食的foodtype有關連性，這時就能導入prototype屬性。


```
function fastfood(name){

　　　　this.name = name;
　　}

　　fastfood.prototype = { foodtype : '主餐' };

   var fastfooda = new fastfood('BaconBurger');

   var fastfoodb = new fastfood('BeefBurger');

   console.log(fastfooda.foodtype);//主餐
   console.log(fastfoodb.foodtype);//主餐

```
现在，foodtype屬性放在prototype對象裡，是兩個實例對象共享的。只要修改prototype对象，就會同时影響兩個實例對象。

做個最後小測試，此時修改prototype，看看結果如何?
```
    fastfood.prototype.foodtype = '加點';
    console.log(fastfooda.foodtype);
    console.log(fastfoodb.foodtype);
```
兩個速食就同時變為加點了!

**由於所有的實例对象共享同一個prototype對象，那麼從外界看起来，prototype對象就好像是實例對象的原型，而實例對象則好像"继承"了prototype對象一樣。**


參考資料:
1. [Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
2. [該來理解 JavaScript 的原型鍊了](https://blog.techbridge.cc/2017/04/22/javascript-prototype/)
