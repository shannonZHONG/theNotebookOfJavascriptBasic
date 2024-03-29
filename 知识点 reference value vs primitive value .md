## 数据种类以及 5个falsy值：<br> 
七种在JavaScript的数据类型：<br>
number string boolean symbol null undefined object;<br>
五个falsy值：<br>
0  NaN “ ” (空字符串) null undefined<br>
七种数据类型 与 五个falsy 值的联系：<br>
symbol 不考虑;<br>
boolean: true /false false 并没有算在 falsy 值里面;<br>
Number: 0 NaN;<br>
String: 空字符串;<br>
null undefined;<br>
所有的object 都是 true;<br>


## 1.0 数据存在stack 和 heap 的差别  <br>
primitive value 存储在memory 的stack 里面；存在stack的值是固定的<br>
reference value 存储在memory 的heap 里面 但reference value 本身存在stack里面；<br>
由于object 的大小常常会改变 改变的时候只要在heap 中allocate 一块新的记忆空间 然后让stack 中的引用指向它就好了<br>
primitive value：undefined null number  string boolean<br>
reference value: object<br>

## 2.0 一个关于临时对象的例子<br>


```
 var s = "hello";// s 的值已经固定 
 s += ",world";// 添加了新的之后 原来的s里面的值 就不再使用 
 console.log(s); // "hello,world"
      
```

 string number boolean  对应到 primitive wrapper value <br>
 primitive value 在被读取之前 会被动态的包裹起来 包裹起来之后 就是 一个object 这个object 也是一个临时对象  所以才会有 properties  and methods<br>
 
 
```
var length = "hello,world!".length;

包裹起来之后 

var length = String("hello,world!").length;// 只是在这一行有效  过行作废 

var book = “test”;
book.author = "test";
console.log(book.author);// undefined 

    
```


## 3.0  例题 <br>

      ``` 
      函数的参数分别为 primitive value 和 reference value 时 的差别：
      var i = 0; // primitive value 
      var j = 0;
      i++;
      console.log(j);
      
      
      var i = 0;
      var f = function(i) {
            z = i + 1；
            console.log(" this is z value " + " " + z)
      };
      f(i);
      console.log(" this is i value  " + " " + i);
    
      ``` 

        
      ```         
     
      var userA = {  // reference value 
            name: "hello"
      };
      
      /* stack 中有两个reference value 指向 同一块 heap 中的地址 所以更改
         it does not create a new object it just have an alias to the original object that is by reference
         in other way ： by reference mean： the objectA is in address 100 and the objectB is in address 100 too. so the objectA is              referenced by ObjectB 
      */
      var userB = userA; 
      userA.name = "changed";
      console.log(userB.name);
  
  
  
       function setName(obj) {
            obj.name = "test";
            obj = new Object(); 
            // 当函数内部重写obj，这个变量引用的就是一个局部对象，而这个局部对象会在函数执行完毕之后立即撤销
            obj.name = "changed"
        }
        var person = new Object();
        setName(person);
        console.log(person.name); // "test"    
        
        
        
        function setName(obj) {
            obj.name = "test";
        }
        var person = new Object();
        setName(person); // obj 和person 引用的是引用的是同一个对象  或者是 它们在stack 的地址都指向heap 里面的同一个东东  而这个东东就是         全局对象 
        console.log(person.name); // "test"            
        
        ```
        
  
    
        ```
         var a = {
            "name": "a"
        };
        b = a;
        b = {
            "name": "b"
        };  // 在 heap 里面重新开辟一个新的存储空间 然后在stack 里的reference 指向这个新的存储空间 
        console.log(a.name);// "a"
        
        
        var a = {
            "name": "a"
        };
        b = a; // 在stack 里面的a 和 b 指向在heap 里面的同一个存储地址 
        b.name = "changed"; 
        a.name;//changed 

        
        var a = {
            "name": "a"
        };
        b = a;
        b = null；
        console.log(a);// "name":"a"

        
        var a = {
            n: 1
        };
        
        var b = a; 
        
        a.x = a = {n: 2}; // 这样写代码不好 在这句话当中事实上有 两个a 或者说 有两个存储a的地方 
        
        console.log(a.x);// 在新的a 里面 没有 x 这个属性 所以 是undefined 
        console.log(b.x); // 在原来的那个a 里面 x 存储的是 一个object 所以打印出来的也是一个object        

        
        var a = {};
        a.self = a;
        console.log(a.self);//  object 
        
        var b = {
        self: b
        };
        // var hosting first and var have value later 
        console.log(b.self);// undefined 
        // 等同于 
        var test;
        test = {self: test};// test have undefined and address of storage  等同于{self: undefined}
       
       
       
       
       
       
      ```



