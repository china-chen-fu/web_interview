#### 数据类型的判断

- 提交分支的判断
  - 所有基本类型中Boolean值是false的只有6个，分别是 :**0 NaN ' ' null undefined false** 引用类型Boolean值全是true

- 基础数据类型的判断使用typeof

  ```js
  (typeof 2)=='number'  //true
  ```

- `instanceof` 只能判断引用类型，而不能判断基本数据类型，内部执行的机制是判断其原型链中是否可以找到该类型的原型

  - ```js
    console.log([] instanceof Array);                    // true
    console.log(function(){} instanceof Function);       // true
    console.log({} instanceof Object);   
    ```

- constructor 似乎完全可以应对基本数据类型和引用数据类型 但如果声明了一个构造函数，并且把他的原型指向了 Array 的原型，所以这种情况下，constructor 也显得力不从心

  - ```js
    console.log((true).constructor === Boolean); // true
    console.log(('str').constructor === String); // true
    console.log(([]).constructor === Array); // true
    console.log((function() {}).constructor === Function); // true
    console.log(({}).constructor === Object); // true
    console.log((2).constructor === Number); // true
    ```

- Object.prototype.toString.call() 完美的解决方案，可以通过toString() 来获取每个对象的类型，

  **`Object.prototype.toString.call()` **使用 Object 对象的原型方法 toString 来判断数据类型：

  - ```js
    var a = Object.prototype.toString;
     
    console.log(a.call(2));
    console.log(a.call(true));
    console.log(a.call('str'));
    console.log(a.call([]));
    console.log(a.call(function(){}));
    console.log(a.call({}));
    console.log(a.call(undefined));
    console.log(a.call(null));
    
    function judgeType(item){
        const a=Object.prototype.toString
        return a.call(item).slice(8,-1)
    }
    ```

#### 数据类型的转换

- 转换为数字

  - ```js
    Number()：可以把任意值转换成数字，如果要转换的字符串中有不是数字的值，则会返回NaN
    ​
    Number('1')   // 1
    Number(true)  // 1
    Number('123s') // NaN
    Number({})  //NaN
    
    
    parseInt(string,radix)：解析一个字符串并返回指定基数的十进制整数，radix是2-36之间的整数，表示被解析字符串的基数。
    parseInt('2') //2
    parseInt('2',10) // 2
    parseInt('2',2)  // NaN
    parseInt('a123')  // NaN  如果第一个字符不是数字或者符号就返回NaN
    parseInt('123a')  // 123
    
    parseFloat(string)：解析一个参数并返回一个浮点数
    ​
    parseFloat('123a')
    //123
    parseFloat('123a.01')
    //123
    parseFloat('123.01')
    //123.01
    parseFloat('123.01.1')
    //123.01
    
    隐式转换
    let str = '123'
    let res = str - 1 //122
    str+1 // '1231'
    +str+1 // 124
    ​
    转换为字符串
    .toString()  ⚠️注意：null,undefined不能调用
    ​
    Number(123).toString()
    //'123'
    [].toString()
    //''
    true.toString()
    //'true'
    ​
    ​
    String() 都能转
    String(123)
    //'123'
    String(true)
    //'true'
    String([])
    //''
    String(null)
    //'null'
    String(undefined)
    //'undefined'
    String({})
    //'[object Object]'
    ​
    ​
    隐式转换：当+两边有一个是字符串，另一个是其它类型时，会先把其它类型转换为字符串再进行字符串拼接，返回字符串
    ​
    let a = 1
    a+'' // '1'
    转换为布尔值
    0, ''(空字符串), null, undefined, NaN会转成false，其它都是true
    Boolean()
    Boolean('') //false
    Boolean(0) //false
    Boolean(1) //true
    Boolean(null) //false
    Boolean(undefined) //false
    Boolean(NaN) //false
    Boolean({}) //true
    Boolean([]) //true
    ​
    条件语句
    ​
    let a
    if(a) {
      //...   //这里a为undefined，会转为false，所以该条件语句内部不会执行
    }
    ​
    隐式转换 !!
    ​
    let str = '111'
    console.log(!!str) // true
     
     
    {}和[]的valueOf和toString的返回结果？
    valueOf：返回指定对象的原始值
    ​
    对象                  返回值 
    Array               返回数组对象本身。
    Boolean             布尔值。
    Date                存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。
    Function            函数本身。
    Number              数字值。
    Object              对象本身。这是默认情况。
    String              字符串值。
                        Math 和 Error 对象没有 valueOf 方法。
    ​
    toString：返回一个表示对象的字符串。默认情况下，toString() 方法被每个 Object 对象继承。如果此方法在自定义对象中未被覆盖，
    toString() 返回 "[object type]"，其中 type 是对象的类型。
    ​
    ({}).valueOf()   //{}
    ({}).toString()  //'[object Object]'
    [].valueOf()    //[]
    [].toString()   //''
    
    
    ```

#### 数据类型的比较

- 数据类型相比较objected .is   ==  和 ===

- ```
  ==操作符的强制类型转换规则
  ​
  字符串和数字之间的相等比较，将字符串转换为数字之后再进行比较。
  其他类型和布尔类型之间的相等比较，先将布尔值转换为数字后，再应用其他规则进行比较。
  null 和 undefined 之间的相等比较，结果为真。其他值和它们进行比较都返回假值。
  对象和非对象之间的相等比较，对象先调用 ToPrimitive 抽象操作后，再进行比较。
  如果一个操作值为 NaN ，则相等比较返回 false（ NaN 本身也不等于 NaN ）。
  如果两个操作值都是对象，则比较它们是不是指向同一个对象。如果两个操作数都指向同一个对象，则相等操作符返回true，否则，返回 false。
  ​
      '1' == 1 // true
      '1' === 1 // false
      NaN == NaN //false
      +0 == -0 //true
      +0 === -0 // true
      Object.is(+0,-0) //false
      Object.is(NaN,NaN) //true
  ```

- typeof null 的结果是什么，为什么？	

  - typeof null 的结果是Object。

    **在 JavaScript 第一个版本中，所有值都存储在 32 位的单元中，每个单元包含一个小的 类型标签(1-3 bits)** 以及当前要存储值的真实数据。类型标签存储在每个单元的低位中，共有五种数据类型

  - ```js
    000: object   - 当前存储的数据指向一个对象。
      1: int      - 当前存储的数据是一个 31 位的有符号整数。
    010: double   - 当前存储的数据指向一个双精度的浮点数。
    100: string   - 当前存储的数据指向一个字符串。
    110: boolean  - 当前存储的数据是布尔值。
    ```

    

  - 有两种特殊数据类型：

    - undefined的值是 (-2)30(一个超出整数范围的数字)；
    - null 的值是机器码 NULL 指针(null 指针的值全是 0)

    那也就是说null的类型标签也是000，和Object的类型标签一样，所以会被判定为Object。

- 判断数组和对象是否为空

  - ```js
    //对象判断是否为空
    function ObjectIsNull(obj){
        if(typeof obj !== "object") throw new Error('传入的参数必须是对象')
        let flag=true
        const arr=Object.keys(obj)
        if(arr.length>0)
            flag=false
        return flag
            
    }
    
    //判断数组是否为空
    function arrayIsNull(arr){
        if(!(arr instanceof Array)) throw new Error('传入的参数必须是数组')
        let flag=true
        if(arr.length>0)
            flag=false
        return flag
    }
    ```

#### 各种数据类型之间的重点

##### 数组类型

###### 题目

[数组的创建方式](#数组的创建方式)	

[判断类型是否是数组](#判断类型是否是数组)

###### 解答

- ### 数组的创建方式

  - 使用字面量的方式  最常用 `let arr=[]`
  - 使用数组的构造函数    `let arr=new Array()`   实例化类
  - 定义的时候直接实例化  `let arr=new Array(item1,item2)`
  - 实例化数组的时候 定义数组的长度  `let arr=new Array(3)`

- ### 判断类型是否是数组

  - `Object.prototype.toString.call()` //`[object Array]`
  - `arr.instanceof(Array)`
  - `arr.constructor==Array`  这个Array是window的属性
  - `Array.isArray()`

- ### 数组的深浅拷贝

  - 浅拷贝  回改变原数组 拷贝的只是引用

    - 直接将数组A重新赋值给数组B

  -  深拷贝 不会改变原数组

    - ```js
      //循环实现深拷贝
      var arr1 = [1, 2, 3];
        var arr2 = [];
        for (var i = 0; i < arr1.length; i++) {
           arr2.push(arr1[i]);
       }
       arr1[0] = 4;
       console.log(arr1); //4, 2, 3
       console.log(arr2); //1, 2, 3
      //concat() 数组连接  返回的是 连接后数组的一个副本 新数组
      arrayObj.concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
      var arr1 = [1, 2, 3];
      var arr2 = arr1.concat();
      arr1[0] = 4;
      console.log(arr1); //4, 2, 3
      console.log(arr2); //1, 2, 3
      //slice	
       // arrayObj.slice(start, [end]) 第第二个参数是下表
       //该方法返回一个 Array 对象，其中包含了 arrayObj 的指定部分。不会改变原数组 
      var arr1 = [1, 2, 3];
      var arr2 = arr1.slice(0);
      arr1[0] = 4;
      console.log(arr1); //4, 2, 3
      console.log(arr2); //1, 2, 3
      
      ```

      

- ### 常用的方法

  - 截取   slice substr substring
    - slice 和 substring  （start,end[可选]）
      - start   从第几个字符开始
      - end    结束位置下一个位置
      - slice(0) 返回整个字符串 从0开始到最后一个字符
      - slice的end是负值 需要加上字符串长度转换为正值
      - substring() 是较大较小值之间的差值1  遇到负数回将它转为正的
    - substr  (start,length)
      - start 开始位置的下标
      - 截取的长度
      - length不写也是默认截取到最后一个字符

