test

数组 [{value: 'a'},{value: 'b'},{value: 'c'},{value: 'd'},{value: 'e'}]根据['b', 'c', 'd', 'a', 'e'] 进行排序（没有数据重复）输出结果为[{value: 'b'},{value: 'c'},{value: 'd'},{value: 'a'},{value: 'e'}]



```js
const sort = (arrObj,arr) => {
  let i = 0;
  const res = [];
  while(res.length < arrObj.length){
    for(let obj of arrObj){
      if(obj.value === arr[i]){
        res.push(obj);
        i++;
      }
    }
  }
  return res;
}
```





```js
// 原始数组
const arr = [{value: 'a'}, {value: 'b'}, {value: 'c'}, {value: 'd'}, {value: 'e'}];

// 目标排序顺序
const order = ['b', 'c', 'd', 'a', 'e'];

// 创建映射表，记录每个值在目标排序数组中的索引位置
const orderMap = {};
order.forEach((value, index) => {
  orderMap[value] = index;
});

// 使用自定义排序函数进行排序
const sortedArr = [...arr].sort((a, b) => {
  return orderMap[a.value] - orderMap[b.value];
});


console.log(sortedArr);

```

