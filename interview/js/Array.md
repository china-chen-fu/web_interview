#### 1. `some()`

- 参数
  - func(currentValue,index,arr) required  必须回调函数
    - currentValue required 当前值
    - index             optional  当前值的索引
    - arr	              optional 当前越苏属于的数组对象
  - thisValue   optional 对象作为改执行回调时使用，传递给函数，用作this的值 省略为undefined
- 返回值
  - 有满足条件的返回true,否则返回false
- 说明
  - some() 方法用于检测数组中的元素是否满足指定条件（函数提供）。
  - some() 方法会依次执行数组的每个元素：
    - 如果有一个元素满足条件，则表达式返回*true* , 剩余的元素不会再执行检测。
    - 如果没有满足条件的元素，则返回false。
- 注意
  - **注意：** some() 不会对空数组进行检测。
  - **注意：** some() 不会改变原始数组。

#### 2. `concat()`

- 参数

  - *array1*.concat(*array2*,*array3*,...,*arrayX*)

- 返回值

  - 返回一个新的数组。该数组是通过把所有 arrayX 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的元素，而不是数组。

- 说明

  - concat() 方法用于连接两个或多个数组。

    该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

- 代码

  - 一道面试题：传递两个参数m，n，返回长度为m，所有元素都为n的数组，要求不能用循环。

    利用函数的递归和 concat() 方法可以实现，代码如下：

  - ```js
    function fn(m,n){
        return m?fn(m-1,n).concat(n):[]
    }
    
    ```

  - `concat()`复制的副本是浅拷贝

- 注意

  - `concat()`里面的参数可以是数组，也可以是元素





