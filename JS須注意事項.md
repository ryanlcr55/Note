### JS 須注意事項

#### null 與 undefined     
typeof    
```
typeof null        // object
typeof undefined   // undefined
```       
      

比較運算    
```
null  == undefined // true
null === undefined // false
```     


#### 箭頭函式 (Arrow function)

```
const calculate = {
  array: [1, 2, 3],
  sum: () => {
    return this.array.reduce((result, item) => result + item)
  }
}
```   

箭頭函式特性: 這邊的 `this.array` 是`抓不到`的!     
也就是說箭頭函示沒有原型(prototype)     
```
var Foo = () => {};
console.log(Foo.prototype); // undefined
```

