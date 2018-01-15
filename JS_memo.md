### 比较运算符:
* ==：该运算符比较会自动转换数据类型再比较，比如

        false == 0; //true

* ===(!==)：该运算符比较不会自动转换数据类型，类型不一致为false,如果一致再进行比较,比如

        false === 0; //false

* NaN：能判断NaN(无法计算结果)的方法只有使用isNaN()函数，如

        isNaN(NaN); //true

----

### strict模式:
一个变量没用var申明则会被认为是全局变量，使用strict模式时若未用var申明变量则报错.
如果支持该模式的浏览器运行则会启用strict模式,启用该模式方法为在JS第一行写

    'use strict';

---

### 字符串:
* 如果浏览器支持ES6模板字符串，则可不使用+号连接字符串，而改用${}

        var name = 'Tom';
    
        console.log(\`My name is ${name}\`);  //My name is Tom,注意不是单引号'而是`

* 一些字符串方法，调用这些方法不会改变原有内容，而是返回一个新字符串.

        var a = '13579';

        a.split(3);  //['1','579'],根据参数分割字符串

        var s = 'Hello,world!';

        s.toUpperCase();  //'HELLO,WORLD!'

        s.toLowerCase();  //'hello,world!'

        s.indexOf('world');  //返回6，搜索指定字符串第一次出现的位置，若不存在则返回-1

        s.substring(0,5);  //'Hello'，返回指定区间的子串

---

### 数组:
* JS的数组越界时不会报错，如通过索引赋值时如果越界赋值结果如下.

        var arr = [1,2,3];
    
        arr[4] = 4; //[1,2,3,undefined,4]

* 一些数组方法:

        var arr = [1,2,3,'a'];

        arr.indexOf(3);  //返回2，搜索指定字符串出现的位置，若不存在则返回-1

        arr.slice(0,3);  //返回[1,2,3]，如String的subString()

        arr.slice(2);  //返回[3,'a']，无参数时则返回所有元素，可用这点复制一个数组

        arr.push('b'); //返回5，往数组末尾添加元素并返回长度

        arr.pop();  //返回'b'，删除数组末尾元素并返回被删元素

        arr.unshift(0);  //返回5，往数组头部添加元素并返回长度

        arr.shift();  //返回0,删除数组头部元素并返回被删元素

        arr.reverse();  //返回['a',3,2,1]，反转数组元素，会直接修改数组本身

        arr.splice(1,2,'b','c'); //返回[3,2]，从索引1开始删除2个元素，并从索引1开始添加2个元素，返回被删数组
 
        arr.splice(3,0,'d');  //返回[]，因为没删除元素所以返回空数组，arr现为['a','b','c','d',1]

        arr.concat([2,3]); //返回一个连接了arr和[2,3]的数组，arr本身不改变

        arr.join('-');  //返回'a-b-c-d-1'，用指定的字符串把数组元素连接起来，并返回连接后的字符串

---

### Map与Set



* Map是一组键值对的结构，具有极快的查找速度。
* 初始化Map需要一个二维数组，或者直接初始化一个空Map，以下为初始化以及方法例子.

        //var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);

        var m = new Map(); // 空Map
    
        m.set('Adam', 67); // 添加新的key-value
    
        m.set('Bob', 59);
    
        m.has('Adam'); // 是否存在key 'Adam': true
    
        m.get('Adam'); // 67
    
        m.delete('Adam'); // 删除key 'Adam'

* Set跟Map相比去掉了value，也具有极快的查找速度。
* 初始化Set需要一维数组，或者直接初始化一个空Set，以下为初始化以及方法例子.

        var s1 = new Set();  // 空Set

        var s2 = new Set([1, 2, 3]);  //Set {1,2,3}

        s2.add(4);  //Set {1,2,3,4}

        s2.has(4);  //返回true

        s2.delete(4);  //Set {1,2,3}

* forEach(),该方法接收一个函数，每次迭代就自动回调该函数。例子如下.

        var a = new Array('A','B','C');

        function demo(elem, index, array){
        console.log(`a[${index}] = ${elem}, array = ${array}`);
        }
        
        a.forEach(demo);
        //a[0] = A, array = A,B,C
        //a[1] = B, array = A,B,C
        //a[2] = C, array = A,B,C

---

### 函数

* 注意js引擎在行末自动加分号的机制，如下例子。

        function foo() {
            return { name: 'foo' };
        }
        foo();  //{ name: 'foo' }

        function foo() {
            return      // 实际这里自动添加了;
                { name: 'foo' };
        }
        foo();  //undefined

* arguments:它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。

        function foo(x){
            console.log('x='+x);
            for(var i=0;i<arguments.length;i++){
                console.log(`arg ${i}=${arguments[i]}`);
            }
        }
        foo(1,2,3);
        //x=1
        //arg 0=1
        //arg 1=2
        //arg 2=3

* rest:获得定义参数以外的参数,rest参数只能写在最后，前面用`...`标识

        function foo(a, b, ...rest) {
            console.log('a = ' + a);
            console.log('b = ' + b);
            console.log(rest);
        }
        foo(1, 2, 3, 4, 5);
        // a = 1
        // b = 2
        // Array [3,4,5]

* window:不在任何函数内定义的变量就具有全局作用域,JavaScript默认有一个全局对象window，全局作用域的变量实际上被绑定到window的一个属性。

        var msg = 'Hello World!';
        alert(window.msg); // Hello World!

* 命名冲突解决法:把自己的所有变量和函数全部绑定到一个全局变量中。

        var MYAPP = {};
        MYAPP.foo = function(x){return x+1;};
        MYAPP.foo(1);  //2

* 局部作用域：由于JavaScript的变量作用域实际上是函数内部，var无法申明一个局部作用域的变量，这个时候可以用`let`代替。

        function foo() {
            for (var i=0; i<100; i++) {}
            i += 100; // 仍然可以引用变量i
            }

        function foo1() {
            for (let i=0; i<100; i++) {}
            i += 100;  //报错
            }        
        
        foo();  //200
        foo1();  //SyntaxError:

* 解构赋值：使用解构赋值，直接对多个变量同时赋值。

        var [x, ,[y,z]] = [1,2,[3,4]];
        //x=1, y=3, z=4
        
        [x,y] = [y,x];
        //x=3, y=1

        var person = {
        name: '小明',
        age: 20,
        gender: 'male',
        passport: 'G-12345678',
        address:{city:'Shenzhen'}
        };

        var {name,nickname=null,gender:sex,address:{city}} = person;
        //name='小明',
        //当不存在nickname属性时，nickname默认为null,
        //把gender属性命名为sex, sex='male',
        //city='Shenzhen'，注意内嵌属性,保证对应层次一致

* apply：一般情况下，如果要单独调用函数，this会指向全局对象(window)。要指定函数的this指向哪个对象，可以用函数本身的apply方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。

        function getAge() {
            var y = new Date().getFullYear();
            return y - this.birth;
        }

        var xiaoming = {
            name: '小明',
            birth: 1990,
            age: getAge
        };

        xiaoming.age(); // 25
        getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空

另一个与apply()类似的方法是call()，唯一区别是：

    apply()把参数打包成Array再传入；

    call()把参数按顺序传入。

对普通函数调用，我们通常把this绑定为null。比如调用Math.max(3, 5, 4)，分别用apply()和call()实现如下：

    Math.max.apply(null, [3, 5, 4]); // 5
    Math.max.call(null, 3, 5, 4); // 5

可以利用apply()动态改变函数行为，做成装饰器，如下。

        var count = 0;
        var oldParseInt = parseInt; // 保存原函数
        window.parseInt = function () {
            count += 1;
            return oldParseInt.apply(null, arguments); // 调用原函数
        };

        parseInt('10');
        parseInt('20');
        console.log('count = ' + count); // 2

* map：map()方法定义在JavaScript的Array中，我们调用Array的map()方法，传入我们自己的函数，就得到了一个新的Array作为结果。

        var arr = [1,2,3,4];
        arr.map(String);  //['1','2','3','4']

* reduce：Array的reduce()把一个函数作用在这个Array的[x1, x2, x3...]上，这个函数必须接收两个参数，reduce()把结果继续和序列的下一个元素做累积计算,如下：

        [x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)

利用map()和reduce(),把字符串'13579'转为列表[1,3,5,7,9]，再转成整型13579。

        function string2int(s) {
            var a = s.split('').map(function(x){return x-'';});
            return a.reduce(function(x,y){return x*10+y;});
        }

* filter：filter()把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定保留还是丢弃该元素。

        var arr = ['a','b','c','d','a'];
        var r = arr.filter(function (element, index, self) 
        {
            return self.indexOf(element) === index;
        });
        //r=['a','b','c','d']

* sort：JS的sort()方法默认把所有元素先转换为String，根据ASCII码排序，所以如果对数组[3,2,1,10]排序则会变为[1,10,2,3]，sort可接收函数作为参数。

        var arr = [10,20,1,2];

        arr.sort(function(x,y){
                if(x < y){return -1;}
                if(x > y){return 1;}
                return 0;
        });
        arr;  //[1,2,10,20]