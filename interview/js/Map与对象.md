### 1.使用对象出现的一些问题

- 键的隐式转换

  - Object缺少哈希映射，因为对象的键（只允许字符串和符号作为主键）会自动调用`toString`方法将一些类型隐式转换为字符串。

- 不需要继承

  - 使用字面量创建的对象会进行原型继承，如果更改`Object.prototype`会对所有的对象都会产生影响，可能会造成原型污染攻击。
  - 可以使用`Object.create(null)`生成一个不继承任何对象的`Object.prototype`

- 命名冲突

  - 当Object的属性和`Obejct.prototype`有冲突的时候可能会报错

  - `obj.hasOwnProperty(key)`

    - 检测对象是否拥有某个属性，返回true/false

    - 能够区分自生属性和继承属性

    - 没有保护这个属性名，如果这个属性被某个对象的属性名占用，需要外部的`hasOwnProperty`l来获取正确的结果：

    - ```js
      var foo = {
        hasOwnProperty: function() {
          return false;
        },
        bar: 'Here be dragons'
      };
      
      foo.hasOwnProperty('bar'); // 始终返回 false
      
      // 如果担心这种情况，
      // 可以直接使用原型链上真正的 hasOwnProperty 方法
      ({}).hasOwnProperty.call(foo, 'bar'); // true
      
      // 也可以使用 Object 原型上的 hasOwnProperty 属性
      Object.prototype.hasOwnProperty.call(foo, 'bar'); // true
      //上面这个方法等价
      Object.prototype.hasOwnProperty.call(obj, key)
      Object.hasOwn
      ```

      

- 获取长度
  - Object没有提供方便的API来获取大小，需要使用其他方式
    - 键都是字符串或者可枚举键，可以使用Object.keys()并且获取length
    - 需要考虑不可枚举的字符串键，必须使用`Object.getOwnPropertyNames`来获取列表并且获取长度
    - 对符号还有兴趣，可以使用`getOwnPropertySymbols`来显示符号键或者使用，`Reflect.ownKeys`同时获取字符串键和符号键，无论是不是可枚举的
- 迭代（遍历）
  - `for...in`遍历
  - `Object.keys`,`Object.values`,`Object.entries`来获取键和值
  - 插入上没有顺序可言，大多数浏览器证书见按照升序排列并且大于字符串
- 清楚
  - 没有简单的方法删除，必须要使用`delete`操作符进行删除，效率缓慢
- 检查属性是否存在
  - `Object.prototype.hasOwnProperty`和`Object.hasOwn`



