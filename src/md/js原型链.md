## js继承

[上一篇继承](https://wu-yu-pei.github.io/2021/10/05/js%E7%BB%A7%E6%89%BF%E7%9A%846%E7%A7%8D%E6%96%B9%E5%BC%8F/)

代码:

<!--more-->

```js
javascript对象的继承再研究
1. 原型链继承
function Person() {}
Person.prototype.say = function () {
    console.log(this.name)
}
function Student(name, age) {
    this.name = name
    this.age = age
}
Student.prototype = new Person()
var s = new Student('wuyupei', 20)
s.say()
console.log(s)

2.借用构造函数继承   缺点 无法继承父类构造函数上的数据
function Person(name, age) {
    this.name = name
    this.age = age
    this.firent = ['a', 'b', 'c']
}

Person.prototype.say = function () {
    console.log(this.name)
}

function Student(name, age, score) {
    Person.call(this, name, age)
    this.score = score
}
var s = new Student('wuyupei', 20, 99)
console.log(s)
console.log(s.name)
console.log(s.age)
console.log(s.score)
s.say()
3.组合式继承 (原型链式继承和借用构造函数继承相结合)
function Person(name, age) {
    this.name = name
    this.age = age
    this.firend = ['a', 'b', 'c']
}

Person.prototype.say = function () {
    console.log(this.name)
}

function Student(name, age, score) {
    Person.call(this, name, age)
    this.score = score
}
// 这里是关键 结果了借用构造函数继承不能继承构造函数上的属性  但是调用了两次构造函数
Student.prototype = new Person()
var s = new Student('wuyupei', 20, 99)
console.log(s.firend)
4.原型式继承 类似于Object.create()方法
var person = {
    name: 'person',
    age: 100,
    say() {
        console.log(this, na)
    },
}
function content(obj) {
    function f() {}
    f.prototype = obj
    return new f()
}
const s = content(person)
console.log(s)

Object.create()方法 返回值和上面的原型继承一样的哎!
    var person = {
        name: 'person',
        age: 100,
        say() {
            console.log(this, na)
        },
    }
var s = Object.create(person)
console.log(s)

5.寄生式继承(就是给原型式继承(Object.create())在套一个壳子)
function createAuthor(obj) {
    var clone = Object.create(obj)
    clone.flag = 'clone'
    return clone
}
var Person = {
    name: 'wuyupei',
    age: 100,
}
var s = createAuthor(Person)
console.log(s)
6.寄生组合式继承
function Person(flag) {
    this.flag = flag
}
Person.prototype.say = function () {
    console.log(this.name)
}

var content = Object.create(Person.prototype) // 继承父构造中的属性

function Student(score) {
    this.score = score
    Person.call(this, 'student') // 借用构造函数 继承属性
}

var s = new Student(20)
console.log(s)
ES6继承
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    say() {
        console.log(this.name)
    }
}

class Student extends Person {
    constructor(name, age, type) {
        super(name, age)
        this.type = type
    }
    sayType() {
        console.log(this.type)
    }
}
var s = new Student('wuyupei', 20, 'sudent')
console.log(s)
s.say()
s.sayType()
```

