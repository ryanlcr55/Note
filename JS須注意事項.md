### JS 須注意事項

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
