---
title: 一些js代码
date: 2019-02-28 14:31:04
tags: 知识
categories: 知识
description: 一些知识
thumbnail: /img/p9.jpeg
toc: true
---

### 统计数组中元素出现次数

    reduce() 方法对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值。
    reducer 函数接收4个参数:

    1.Accumulator (acc) (累计器)
    2.Current Value (cur) (当前值)
    3.Current Index (idx) (当前索引)
    4.Source Array (src) (源数组)
    您的 reducer 函数的返回值分配给累计器，该返回值在数组的每个迭代中被记住，并最后成为最终的单个结果值。

    
    ```

    const count = arr => arr.reduce((acc, val) => {
        acc[val] = (acc[val] || 0) + 1;
        return acc;
    },{})
    count([1,1,2,3,1,1,2]); // {1:4,2:2,3:1}

    ```

### 数组扁平化(完全)
    concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

    
    ```

    const aryFlatten = arr => [].concat(...arr.map(v => Array.isArray(v) ? aryFlatten(v) :v))
    
    reduce版
    const aryFlatten = arr => arr.reduce((a, v) => a.concat(Array.isArray(v) ? aryFlatten(v) : v),[])
    
    aryFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]

    ```

### 根据提供的层数扁平化
    
    ```

    const flattenBy = (arr, depth=1) => arr.reduce((a, v) => a.concat(depth>1 && Array.isArray(v) ? flattenBy(v, depth-1) : v),[])
    flattenBy([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]

    ```

### 去除数组中的所有假植
    
    ```

    const filterFalsy = arr => arr.filter(Boolean)
    filterFalsy(['', true, {}, false, 'sample', 1, 0]); // [true, {}, 'sample', 1]
    
    ```

### 获取指定值在数组中出现的所有下标
    
    ```

    const indexOfAll = (arr, val) => arr.reduce((a, v, i) => v===val? [...a,i]: a,[])
    indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
    
    ```

### 通过给定的结束值，开始值，步长生成数组
    Array.from() 方法从一个类似数组或可迭代对象中创建一个新的数组实例。
    Math.ceil 向上取整

    
    ```

    const initializeArrayWithRange = (end, start=0, step=1) => 
    Array.from({length: Math.ceil(end-start+1)/step}, (v, i)=> i*step+start)
    
    initializeArrayWithRange(5); // [0,1,2,3,4,5]
    initializeArrayWithRange(7, 3); // [3,4,5,6,7]
    initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]

    ```


### 获取两个数组的交集
    
    ```

    const intersection = (a, b) => {
        const s = new Set(b)
        return a.filter(x => s.has(x))
    }
    或
    const intersection = (a, b) => a.filter(x => b.includes(a))

    intersection([1, 2, 3], [4, 3, 2]); // [2, 3]
    
    ```

### 打乱数组顺序
    
    ```

    const shuffle = arr =>{
        let m = arr.length;
        while(m){
            let i = Math.floor(Math.random() * m--)
            [arr[i],arr[m]] = [arr[m],arr[i]]
        }
        return arr;
    }
    shuffle([1, 2, 3]); // [2, 3, 1]

    ```

### 根据提供的方法留下符合条件的
    
    ```

    const uniqueElementsBy = (arr, fn) => arr.reduce((acc, val) => {
        !acc.some(x => fn(x,val))?acc.push(val):''
        return acc;
        }
        ,[])
        
    uniqueElementsBy(
    [
        { id: 0, value: 'a' },
        { id: 1, value: 'b' },
        { id: 2, value: 'c' },
        { id: 1, value: 'd' },
        { id: 0, value: 'e' }
    ],
    (a, b) => a.id == b.id
    );
    返回 [ { id: 0, value: 'a' }, { id: 1, value: 'b' }, { id: 2, value: 'c' } ]
    
    ```

### 防抖
    ```

    const debounce = (fn, ms=0)=>{
        let timer;
        return fn(...args){
            clearTimeout(timer);
            timer = setTimeout(() => fn.bind(this,args),ms)
        }
    }

    ```
### 先立即执行一次再防抖
    
    ```

    const debounce = (fn, ms=0, immediate=true)=>{
        let timer;
        return function(...args){
            if(timer) clearTimeout(timer)
            if(immediate){
                fn()
                immediate=false
            }else{
                timer = setTimeout(()=>{
                    fn.apply(this,args)
                    immediate=true
                },ms)
            }
        }
    }
    
    ```

### 斐波那契
    
    ```

    const fb = (n) => Array.from({length:n+1}).reduce((acc,val,i) => 
        (acc.concat(i>1?acc[i-2]+acc[i-1]:i)),[])
    
    ```

### 先立即执行一次再节流
    
    ```

   const throttle = (fn, wait) => {
    let inThrottle, lastFn, lastTime;
    return function() {
        const context = this,
        args = arguments;
        if (!inThrottle) {
        fn.apply(context, args);
        lastTime = Date.now();
        inThrottle = true;
        } else {
        clearTimeout(lastFn);
        lastFn = setTimeout(function() {
            if (Date.now() - lastTime >= wait) {
            fn.apply(context, args);
            lastTime = Date.now();
            }
        }, Math.max(wait - (Date.now() - lastTime), 0));
        }
    };
   };
    
    ```

### 只执行一次的方法
    
    ```

    const once = fn => {
        let called = false;
        return fn(...args){
            if(called) return;
            called = true;
            return fn.apply(this,...args)
        }
    }
    
    ```

### 生成指定范围内的n个随机数
    
    ```

    const randomIntArrayInRange = (max, min, n) => 
    Array.from({length:n},()=> Math.floor(Math.random() * (max-min+1) + min)))
    
    ```

### 深拷贝
    
    ```

    const deepClone = obj => {
    let clone = Object.assign({}, obj);
    Object.keys(clone).forEach(
        key => (clone[key] = typeof obj[key] === 'object' ? deepClone(obj[key]) : obj[key])
    );
    return Array.isArray(obj) && obj.length
        ? (clone.length = obj.length) && Array.from(clone)
        : Array.isArray(obj)
        ? Array.from(obj)
        : clone;
    };
    
    ```
