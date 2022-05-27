# TypeScript



## 类型

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207114724467.png" alt="image-20220207114724467" style="zoom:50%;" />

高级类型：union组合类型，Nullable可空类型，Literal预定义类型

```typescript
function add(n1: number, n2: number) {
  return n1 + n2
}

//通过上下文自动适配类型
let isTrue = true;
isTrue = "true"

//也可以显示指定类型
let isTrue: boolean = true;
let total: number = 0;
let firstName: string = "Lyle";
let str = `My name is ${firstName}`

```



Array和Tuple

```typescript
//这三种方式声明的数组完全一样
let list1: number[] = [1,2,3,4]
let list2: Array<number> = [1,2,3,4]
let list3 = [1,2,3,4]

//实现JS里面的数组
let list4 = [1, "add"]
let list5: any[] = [1,"dss",true]


//Tuple是一个特殊的数组，固定长度和类型的数组
//声明Tuple时一定要指定类型和长度，不然就是数组
let person1: [number,string] = [1,"Lyle"]
person[0] = "add"  //error
person[1] = 1 //error

//Tuple存在一个bug
person1[2] = 3
//这样竟然不会报错
person1.push(3)



//一个变量同时支持两种类型
let union: string | number
union = 2
union = "sdsdsds"

let union2: nubmer | string | boolean | string[]
function merge(n1: number | string, n2: nubmer | string) {
  if (typeof n1 === "string" || typeof n2 === "string") {
    return n1.toString() + n2.toString()
  } else {
    return n1 + n2
  }
}


//literal字面量类型
function merge(n1: number | string, n2: nubmer | string, resultType: "as-number" | "as-string") {
  if (resultType === "as-string") {
    return n1 + n2
  }
  if (typeof n1 === "string" || typeof n2 === "string") {
    return n1.toString() + n2.toString()
  } else {
    return n1 + n2
  }
}

let mergeNumber = merge(2, 5, "as-number")

```





Enum枚举类型

枚举里面实际上是数字类型，从0开始

```typescript
enum Color {
  red = 5,
  green,
  blue
}

let color = Color.blue

```





Any 与 unknown

```typescript
let randomValue: any = 6666
randomValue = true;
randomValue = "ss";
randomValue = {}
randomValue()


//unkonwn和any很相似，但需要检查类型在使用前
let randomValue: unknown = 6666
randomValue = true;
randomValue = "ss";
randomValue = {}
if (typeof randomValue === 'function') {
  randomValue()
}

```



void, undefined, never

```typescript
//void 就是表示没有哈


```





## 面向对象

```typescript
interface IPoint {
  x: number;
  y: number;
  drawPoint: () => void;
  getDistances: (p: IPoint) => number;
  
}

class Points implements IPoint {
  //x: number;
  //y: number;
  
  constructor(public x: number, public y: number) {
   // this.x = x;
   // this.y = y;
  }
  drawPoint = () => {
    console.log(this.x, this.y)
  }
  getDistances = (p: IPoint) => {
    return ...
  }
}

const point = new Point();
point.drawPoint()
  
```

注意构造函数无法重载，只有一个构造函数，



gettter 和 settter 懒人包





## 泛型

```typescript
let lastInArray = <T>(arr: T[]) => {
  return arr[arr.length - 1]
}

const l1 = lastInArray([1,2,3,4]);
const l2 = lastInArray(["a","b","c"]);
const l3 = lastInArray<string | number>(["a","b","c"]);
```



