let定义：

​	1、没有域解析，不纯在变量提升

​		在代码块内，只要let定义变量，在之前使用都是报错

​		先定义在使用

​	2、同一个作用域里面，不能重复定义变量

​	3、for循环，for循环里面是父级作用域，里面又一个

​	4、var声明的变量是属于window的let和const不是

```javascript
{
  let a = 12;
  {
    let a = 6
    console.log(a) //6
  }
  console.log(a) //12
}

var arr = [];
	for (let i = 0; i < 10; i++) {
		arr[i] = function() {
			console.log(i)
		}
	}
	arr[1]();
```

解构赋值：

```javascript
let [a,b,c] = [12,1,2];

	let [d,e,f = '暂无数据'] = ['a','b']
	console.log(a,b,c)
	console.log(d,e,f)

	let json = {
		name:'strive',
		age:20,
		sex:'nan'
	}
	let {name:n,age:g,sex} = json
	console.log(n,g,sex)

	let q = 12,w = 5;
	[q,w] = [w,q];
	console.log(q,w)

	function getposition() {
		return {
			t:30,
			l:100
		}
	}
	({t,l} = getposition());
	console.log(t,l)

	function show({a,b,c='默认'}){
		console.log(a,b,c)
	}
	show({
		a:1,
		b:2
	})
```



字符串模板：

​	可以随意的换行`${data}`	

字符串查找：

​	indexof str.indexof(要找的东西)  返回值  索引的位置 没找到返回的-1

​	includes() str.includes(要找的东西)  返回值 true/false

```javascript
if (navigator.userAgent.includes('Chrome')) {
		console.log('yes')
	}else {
		console.log('no')
}
```

字符串检测是已谁开头的:

```javascript
let str = 'file:///Users/mac/Downloads/es6demo1.html';
let str2 = 'https://www.zhihu.com/';
console.log(str2.startsWith('http'))
```

字符串检测是已谁结尾的:

```javascript
let sss = 'aaa.png';
let ssss = 'aaa.html';
console.log(ssss.endsWith('png'))
```

字符串重复多少次:

```javascript
let strs = '重复'
console.log(strs.repeat(1000))
```

字符串填充:
	 padStart(字符串长度，填充的字符串) 往前添加
	 padEnd(字符串长度，填充的字符串) 往后添加

```javascript
let str5 = 'apple';
let startpad = 'xxx';
console.log(str5.padStart(str5.length+startpad.length,startpad))
console.log(str5.padEnd(str5.length+startpad.length,startpad))
```

函数：

​	函数默认参数已经定义，不能在使用let或者const声明

默认值函数:

```javascript
function show2({a=111,b=222}={}) {
		console.log(a,b);
}
show2()
```

扩展运算符,reset运算符:

```javascript
let arrs1 = [1,2,3,4,5];
console.log(...arrs1);

function shows1(a,b,c) {
	console.log(a,b,c);
}
shows1(...[1,2,3])

function shows2(...a) {
	console.log(a.sort());
}
shows2(1,9,-3,2)

function shows3(a,b,...c) {
	console.log(a,b)
	console.log(c)
}
shows3(1,2,3,4,5)

// 复制一份数组
let arrss1 = [1,2,3,4,5,6];
let arrs2 = [...arrss1];
console.log(arrss1,arrs2);
// ...:
// 	[1,2,3,4,5] -> ...[1,2,3,4,5] -> 1,2,3,4,5
// 	1,2,3,4,5 -> ...1,2,3,4,5 -> [1,2,3,4,5]
// 剩余参数：必须放到参数末尾
```

箭头函数:

```javascript
let jiantou = (a,b) => {
			return console.log(a+b)
}
jiantou(20,3)
// 注意
	// 1、this问题，定义函数所在的对象，不在是运行时所在的对象
let jsonss3 = {
			id:1,
			sex:() => {
					// 箭头函数里的this这时候指向window
					console.log(this.id)
			}
}
jsonss3.sex();
	// 2、箭头函数里面没有arguments,使用...可以代替arguments
function jiantousssss() {
			console.log(arguments)
}
jiantousssss(1,2,3,4,5)
			let jiantou2 = (...argus) => {
			console.log(argus)
}
jiantou2(1,2,3,4,5)
// 3、箭头函数不能当构造函数
function jiantou3() {
			this.name = 'abc'
}
let ns = new jiantou3();
console.log(ns.name);
let jiantou4 = () => {
				this.name = 'abc'
};
let ns1 = new jiantou4
console.log(ns1.name)
```



数组：

​	循环：

```javascript
// forEach
		let arrEach = ['apple','bannene','oringe','tomato'];
		arrEach.forEach((value,index,arr) => {
			console.log(this,value,index,arr)
		},123)
		// forEach(循环的回调函数，this指向谁,箭头函数除外箭头函数只能指向他的父级)
	// map
		// 做数据映射，正常情况下需要配合return，返回的是一个新的数组若没有return，相当于forEach只要使用map一定要有return
	// filter
		// 过滤一些不合格的元素，如果回调函数是true就留下来false就放弃
	// some
		// 类似查找，数组里面某一个元素符合条件，返回true否则false
	// every
		// 数组里面所有的元素都要符合条件，才返回true否则false
	// reduce 从左往右
		// 求数组的和，积，阶乘
			let arrreduce = [1,2,3,4,5,6,7,8,9,10];
			let arrduce = arrreduce.reduce((prev,cur,index,arr)=>{
				return prev+cur;
			})	
console.log(arrduce)	
// reduceRight 从右往左
	// 求数组的和，积，阶乘
// 幂的运算符
// Math.pow(2,3)===2**3
```

新增数组：

```javascript
// Array.from有length就可以转换成数组类数组转换成数组
		function arrform(){
			let arrgs1 = Array.from(arguments);
			console.log(arrgs1);
		}
		arrform(1,2,3,4,5,6)

//Array.of 把一组值转换成数组
		let arrof = Array.of('apple','bannene','oringe');
		console.log(arrof);
// arr.find()查找，找出第一个符合条件的数组成员如果没有找到就返回undefined
		let arrlength = [20,900,101,100]
		let arrfind = arrlength.find((item,index,arr)=> {
			return item >100;
		})
		console.log(arrfind)
// arr.findIndex()查找的是位置下标，没有找到的是-1
		let arrfindIndex = arrlength.findIndex((item,index,arr)=> {
			return item >100;
		})
		console.log(arrfindIndex)
// arr.fill(填充的东西，开始位置，结束位置)
		let arrfill = new Array(10);
		arrfill.fill('默认添加',2,8);
		console.log(arrfill)
// arr.includes()包含检测数组中是否有这个元素如果有返回true 如果没有是false
		let arrincludes = ['apple','oringe','banben'];
		console.log(arrincludes.includes('oringe2'))
```



对象：json

```javascript
// 对象简介语法,在里面不要使用箭头函数
			let names = 'zhangsan';
			let agex = 18
			let jsones = {
				names,
				agex,
				showa(){
					console.log(this.names)
				}
			}
			console.log(jsones.showa())
// Object.is()用来比较两个值是否相等
			console.log(Object.is(1,1))
// Object.assign(目标对象，source1.source2)复制一个对象，合并参数
			let json1 = {a:1},json2 = {b:2},json3={c:3};
			let objectass = Object.assign({},json1,json2,json3);
			console.log(objectass);
			let objarrass = ['apple','bannene','orange']
			let abjarrsgin = Object.assign([],objarrass)
			console.log(abjarrsgin)
// ...对象身上也可以使用
			let jsondian = {a:1,b:2,c:3}
			let jsondian1 = {...jsondian}
			console.log(jsondian1)
```

Promise:

```javascript
// Promise 解决异步回调问题
		let apromise = 101
		new Promise(function(resolve,reject){
			// resolve成功调用
			// reject失败调用
			if (apromise === 10) {
				resolve('成功了')
			}else{
				reject('失败了！')
			}
		}).then((res)=> {
			console.log(res)
		}).catch((err)=>{
			console.log(err)
		})
// Promise.resolve('aa')将现有的东西，转成一个promise对象，resolve状态，成功状态
		let p1 = Promise.resolve('成功！')
		p1.then(res=> {
			console.log(res)
		})
		let p6 = Promise.resolve('成功！')
		p6.then(res=> {
			console.log(res)
		})
// Promise.reject('aa')将现有的东西，转成一个promise对象，reject状态，失败状态
		let p2 = Promise.reject('失败！')
		p2.catch(res=> {
			console.log(res)
		})
// Promise.all([p1,p2])把promise打包，扔到一个数组里面，打包完还是一个promise对象，全部成功返回成功有一个失败就返回失败
		Promise.all([p1,p6]).then((res)=> {
			console.log(res)
		}).catch((err)=> {
			console.log(err)
		})
// Promise.race([p1,p2])把promise打包扔到一个数组里面，打包完还是一个promise对象，第一个成功就返回成功第一个失败就返回失败
		Promise.race([p2,p1,p6]).then((res)=> {
			console.log(res)
		}).catch((err)=> {
			console.log(err)
		})
// promise应用 获取登录状态和用户信息
		let status = 1;
		let userlogin = (resolve,reject)=>{
			setTimeout(()=> {
				if (status===1) {
					resolve({data:'login success',state:0,token:'sjdnajndknasndkas'})
				}else{
					reject('失败1')
				}
			},2000)
		}
		let getuserinfo = (resolve,reject)=> {
			setTimeout(()=> {
				if (status===1) {
					resolve({data:'getuser success1',state:01,token:'asdasdasdasdasd'})
				}else{
					reject('失败2')
				}
			},1000)
		}
		new Promise(userlogin).then((res)=>{
			console.log('用户登录成功')
			return new Promise(getuserinfo)
		}).then(res=> {
			console.log('获取用户信息成功')
		})

```













​	