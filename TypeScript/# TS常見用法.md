# TS常見用法

## enum

-   根據上一個 value 進行+1
-   無法推斷就需要賦值
-   場景 - 為常數進行命名，提高 code 的可讀性。

```
const handleWrongStatus = (status: string): void => {
  switch (status) {
    case 'A':
      // Do something...
      break;
    case 'B':
      // Do something...
      break;
    case 'C':
      // Do something...
      break;
    default:
      throw (new Error('No have wrong code!'));
  }
};
```

```
enum requestStatusCodes {
  error = 400,
  success = 200,
}

enum requestWrongCodes {
  missingParameter = 'A',
  wrongParameterType = 'B',
  invalidToken = 'C',
}
```

```
const handleResponseStatus = (status: number): void => {
  switch (status) {
    case requestStatusCodes.success:
      // Do something...
      break;
    case requestStatusCodes.error:
      // Do something...
      break;
    default:
      throw (new Error('No have status code!'));
  }
};

const handleWrongStatus = (status: string): void => {
  // 如果覺得 requestWrongCodes.missingParameter 太長了，也可以用以下方式：
  const { missingParameter, wrongParameterType, invalidToken, } = requestWrongCodes;
  switch (status) {
    case missingParameter:
      // Do something...
      break;
    case wrongParameterType:
      // Do something...
      break;
    case invalidToken:
      // Do something...
      break;
    default:
      throw (new Error('No have wrong code!'));
  }
};
```

## const enum

-   使用 const 宣告 enum 不會經過 object
-   benefit
    -   降低效能耗損減少使用 IIFE 產生 object，並將 key & value 綁定到 obj 的過程。
    -   就算 Enum 不多，再判斷時也需要一直「從 Object 中找出對應的值」，而如果是用 const 宣告 Enum ，在編譯成 JS 時就將宣告的值直接放入判斷式。
-   缺點
    -   無法反向取值
    -

## 基础类型

常用：boolean、number、string、array、enum、any、void
不常用：tuple、null、undefined、never

## interface & type

interface 可以進行合併宣告，type 不行。
一般使用 interface 宣告，需

```
interface Hero {
  name: string;
  age: number;
  skill: string;
  skinNum?: number;
  say(): string; // say函数返回值为string
  [propname: string]: any; // 当前Hero可定义任意字符串类型的key
}
// 继承
interface littleSoldier extends Hero {
  rush(): string;
}
// 任意类型
interface IAnyObject {
  [key: string]: any;
}

type Hero = {
  name: string,
  age: number,
  skill: string,
  skinNum?: number,
};
```

## Array

```
interface IItem {
  id: number;
  name: string;
  isGod: boolean;
}
const objectArr: IItem[] = [{ id: 1, name: '俊劫', isGod: true }];
// or
const objectArr: Array<IItem> = [{ id: 1, name: '俊劫', isGod: true }];

const numberArr: number[] = [1, 2, 3];

const arr: (number | string)[] = [1, "string", 2];
```

表示接受 number & string 的混合 array

```
const testFunc = <T extends (number | string)[]>(prop: T): T => {
    return prop;
}
```

## 泛型

-   可理解成 placeholder，作為保留擴充性
    -   K（Key）：表示对象中的键类型；
    -   V（Value）：表示对象中的值类型；
    -   E（Element）：表示元素类型。

```
const output = <T,>(value: T): void => {
    console.log(value);
};

// Outputs: 2
output<number>(2);

// Outputs: 'value'
output<string>('value');
```

```
interface IAnimal {
    type: string;
    eat: () => void;
}

class Dog implements IAnimal {
    type = 'dog';

    eat(): void {
        console.log('eating')
    }
}

const output = <T extends IAnimal>(value: T): void => {
    console.log(value);
};


// Outputs: Dog { type: 'dog' }
output(new Dog());
```

## 斷言

指定 value 的型別，確保可以使用特別型別的 method

```
function temp(test: string | (string | number)[]) {
    let a = (test as []).map((e) => { return e })
    return a
}

console.log(temp([1, 3, 68, 54]))
```

若是這邊沒有使用 as 進行斷言就會出錯。

## in

-   型別保護機制
-   in 運算符在 animal 中尋找 skill 的屬性
-   如果有 skill 就推斷為 Waiter
-   沒有就是 Teacher

```
interface Waiter {
  anjiao: boolean;
  say: () => {};
}

interface Teacher {
  anjiao: boolean;
  skill: () => {};
}
```

```
function judgeWhoTwo(animal: Waiter | Teacher) {
if ("skill" in animal) {
animal.skill();
} else {
animal.say();
}
}
```

## function

-   void = 沒有 return
-   never = 不會有結果的 function
    -   無限迴圈
    -   會被中斷的 func ex: (throw new Error)

```
// 定义一个小姐姐
interface IGirl {
  name: string,
  age: number,
  skill: string,
  isAnMo: boolean;
  number: JiShiEnum;
};

// 定义搜索小姐姐的参數
interface ISearchParams extends IGirl{
  serviceTime: string;
}

//return 類型
interface IGetGirls {
  data: IGirl[];
}
// 函数主体
export function getGirls(data: ISearchParams): Promise<IGetGirls> {
  return axios({
    url: `/dabaojian/getGirls`,
    method: 'GET',
    data,
  });
}
```

## 型別檢測

-   typeof
    -   用於獲得目標型別

```
interface Hero {
  name: string;
  skill: string;
}

const zed: Hero = { name: "影流之主", skill: "影子" };
type LOL = typeof zed; // type LOL = Hero。
```

這邊使用 typeof 獲取目標型別，並賦值給 LOL
這時候 LOL 的型別 = zed 的型別

```
const ahri: LOL = { name: "阿狸", skill: "魅惑" };
```

-   instanceof
-   用於檢查目標是否屬於特定的 class
-   語法`object instanceof class`

```
class NumberObj {
  count: number;
}
function addObj(first: object | NumberObj, second: object | NumberObj) {
  if (first instanceof NumberObj && second instanceof NumberObj) {
    return first.count + second.count;
  }
  return 0;
}
```

```
class Animal {
  speak(): void {
    console.log("Animal makes a sound");
  }
}

class Dog extends Animal {
  speak(): void {
    console.log("Dog barks");
  }
}

class Cat extends Animal {
  speak(): void {
    console.log("Cat meows");
  }
}

const dog = new Dog();
const cat = new Cat();

console.log(dog instanceof Dog); // true，因为 dog 是 Dog 类的实例
console.log(cat instanceof Cat); // true，因为 cat 是 Cat 类的实例

console.log(dog instanceof Animal); // true，因为 dog 是 Animal 类的实例的派生类
console.log(cat instanceof Animal); // true，因为 cat 是 Animal 类的实例的派生类

console.log(cat instanceof Dog); // false，因为 cat 不是 Dog 类的实例
console.log(dog instanceof Cat); // false，因为 dog 不是 Cat 类的实例
```

-   keyof
    -   找出 interface 中的 key
    ```
    interface Point{
      x:number;
      y:number;
    }
    type keys = keyof Point;
    ```
    -   應用
        -   可以更好的定義 data 型別
        ```
        function get<T extends object, K extends keyof T>(o: T, name: K): T[K] {
          return o[name]
        }
        ```

## TS 中的 keyword 基本上出現於 class

-   public
-   private 不可繼承 & 不可從外部取用
-   protected 可繼承 不可取用
-   public readOnly xxx 唯讀
-   static funcXXX 靜態 Method 不用 new 就可以取用
-   abstract funcXX 抽象 class，所有 child class 必須實現 funcXX

## TS config

-   https://www.tslang.cn/docs/handbook/tsconfig-json.html

### 作用

-   標示 TS root 目錄
-   配置 TS compiler
-   指定需 compiler 文件

### 注意事項

-   tsc -init 生成 tsconfig.json
-   compilerOptions 內部字串含意
-   project 別名配置 : 坑:只在 project 中 config 配置別名無效，需要再 tsconfig.json 在配置一次

## Utility Types

-   可理解為基於 TS 的封裝工具類型
    -   https://juejin.cn/post/6865910915011706887
    -   https://zhuanlan.zhihu.com/p/120802610

### Partial<T>

將 T 中所有屬性轉為可選屬性，return 可以是 T 的任務子合集

```
export interface UserModel {
  name: string;
  age?: number;
  sex: number;
}

type JUserModel = Partial<UserModel>
// =
type JUserModel = {
    name?: string | undefined;
    age?: number | undefined;
    sex?: number | undefined;
}
```

-   source code

```
type Partial<T> = { [P in keyof T]?: T[P]; };
```

### Required<T>

-   與 Partial 相反 ，將所有屬性變成必選，並建構一個新的 type

```
type JUserModel2 = Required<UserModel>
// =
type JUserModel2 = {
    name: string;
    age: number;
    sex: number;
}
```

### Readonly<T>

將所有屬性設定成唯讀

```
type JUserModel3 = Readonly<UserModel>

// =
type JUserModel3 = {
    readonly name: string;
    readonly age?: number | undefined;
    readonly sex: number;
}
```

...continue

-   https://juejin.cn/post/6981728323051192357#heading-14
