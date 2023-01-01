---
title: "はじめての TypeScript"
emoji: "🔖"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["typescript"]
published: false
---

# 環境構築

## 環境

- [参考](https://www.udemy.com/course/ts-for-js-developers/)
- MacOS
- VSCode
  - Prettier(コードフォーマッター)
    ```
    # package.json と同階層に配置
    $ touch .prettierrc
    ```
    ```yaml
    # 詳細: https://prettier.io/docs/en/options.html
    printWidth: 120 # 1行の文字数制限
    tabWidth: 2
    singleQuote: true
    trailingComma: es5
    semi: true
    ```
  - setting.json(VSCode 本体の設定ファイル)
    ```json
    {
      "editor.detectIndentation": false,
      "explorer.confirmDragAndDrop": false,
      "editor.minimap.enabled": false,
      "explorer.confirmDelete": false,
      "editor.tabSize": 2,
      "git.autofetch": true,
      "workbench.iconTheme": "file-icons",
      "emmet.syntaxProfiles": {
        "javascript": "jsx"
      },
      "emmet.triggerExpansionOnTab": true,
      "window.zoomLevel": 0,
      "javascript.updateImportsOnFileMove.enabled": "always",
      "liveServer.settings.donotShowInfoMsg": true,
      "editor.formatOnSave": true,
      "prettier.semi": true,
      "prettier.singleQuote": true
    }
    ```

````

## nodejs

- [nodebrew](https://github.com/hokaccha/nodebrew)

## github

- https://github.com/takiguchi-yu/type-script-for-javascript-developers

## package.json

```bash
$ npm init -y
````

## TypeScript

- [TypeScript](https://github.com/microsoft/TypeScript)

```bash
$ npm info typescript
typescript@3.8.3 | Apache-2.0 | deps: none | versions: 1566

$ npm install typescript@3.8.3 --save-dev

# typescriptはdevにインストールしたためこのままでは使えない
$ tsc src/install-typescript.ts
zsh: command not found: tsc

# パッケージを直指定をして実行
$ ./node_modules/.bin/tsc src/install-typescript.ts
or
$ npx tsc src/install-typescript.ts
# 生成されたjsを実行
$ node src/install-typescript.js
```

初期化

```bash
npx tsc init
```

- [ts-node](https://github.com/TypeStrong/ts-node)  
  ts ファイルを直接実行するためのツール

```bash
$ npm info ts-node
ts-node@8.5.4 | MIT | deps: 5 | versions: 105
$ npm install ts-node@8.5.4 --save-dev

$ npx ts-node src/install-typescript.ts
```

- [ts-node-dev](https://github.com/whitecolor/ts-node-dev)

```bash
$ npm info ts-node-dev
ライブコーディングするためのツール
ts-node-dev@1.0.0-pre.44 | MIT | deps: 12 | versions: 44
$ npm install ts-node-dev@1.0.0-pre.44 --save-dev

# 実行
$ npx ts-node-dev --respawn src/install-typescript.ts
Using ts-node version 8.9.1, typescript version 3.8.3
```

package.json にスクリプトを登録

```diff
   "scripts": {
+    "dev": "ts-node-dev --respawn",
     "test": "echo \"Error: no test specified\" && exit 1"
   },
```

```bash
$ npm run dev src/install-typescript.ts
```

# 基本的な型(Type)

- boolean ... 真偽値
- number ... 数値
- string ... 文字列
- number[] or Array<number> ... 配列
- number[][] ... 二次元配列
- [string, number] ...tuple 型という
- any ... 基本的には型が不明になってしまうので使用禁止

以下のような json がある場合

```json
{
  "id": 1,
  "title": "title",
  "description": "description",
},
```

以下のような型定義をすることができる
(Article は任意の型文字列)

```js
interface Article {
  id: number;
  title: string;
  description: string;
}
let data: Article[];
```

- void

```js
function returnNothing(): void {
  console.log('I dont return anything.');
}
console.log(returnNothing());
```

- null, undefined

```js
let absence: null = null;
// absence = 'hello'; // Error!!

let data: undefined = undefined;
// data = 123; // Error!!
```

- never ... 呼び元に戻ってこないよ、の意味の型(return なし)

```js
function error(message: string): never {
  throw new Error(message);
}

try {
  let result = error('test');
  console.log('未到達ロジック' + result);
} catch (error) {
  console.log({ error });
}
```

- object

```js
let profile1: object = { name: 'Ham' };
profile1 = { brithYear: 1976 };

// 上記でもObject型を定義できるが、TypeScriptでは以下のようにできるだけ強い型を付けることが推奨されている

let profile2: {
  name: string,
} = { name: 'Ham' };
// profile2 = { brithYear: 1976 }; // Error!!
```

- Type Aliases

```js
type Mojiretsu = string;
const fooMojiretsu: Mojiretsu = 'Hello';

type Profile = {
  name: string,
  age: number,
};
const example1: Profile = {
  name: 'Ham',
  age: 43,
};

// typeofで既存の型をそのまま定義できる
const example2 = {
  name: 'Ham',
  age: 43,
};
type Profile2 = typeof example2;
```

- interface

```js
interface ObjectInterface {
  name: string;
  age: number;
}

let object: ObjectInterface = {
  name: 'Ham-san',
  // name: true, // Error!!
  age: 43,
};
```

- unknown ... typeof と組み合わせて型推論してから処理を実行する(このことをタイプガードという)

```js
const kansu = (): number => 43;
let numberUnknown: unknown = kansu();
let sumAny = numberAny + 7;
if (typeof numberUnknown === 'number') {
  let sumUnknown = numberUnknown + 7;
}
```

- intersection(交差型) ... 複数を合体

```js
type Pitcher1 = {
  throwingSpeed: number,
};
type Batter1 = {
  battingAverage: number,
};
// ２つのタイプ（型）を合体できる
type TwoWayPlayer = Pitcher1 & Batter1;

const OtaniShohei: TwoWayPlayer = {
  throwingSpeed: 154,
  battingAverage: 0.367,
};
```

- union ... 複数の型を許容するための型

```js
let value: number | string = 1;
value = 'foo';
```

- Literal ... 特定の値のみを許容するための型

```js
let dayOfTheWeek: '日' | '月' | '火' | '水' | '木' | '金' | '土';
dayOfTheWeek = '月';
// dayOfTheWeek = '31'; // Error!!
```

- enum

```js
enum Months {
  January = 1,  // 1始まりからを定義できる
  February,     // 2
  March,        // 3
  April,        // 4
}
console.log(Months.April);

enum COLORS {
  RED = '#ff0000',
  WHITE = '#ffffff',
  GREEN = '#008000',
}
console.log(COLORS.GREEN);
```

# 関数で型を使う

- function

```js
function bmi(height: number, weight: number): number {
  return weight / (height * height);
}
console.log(bmi(1.72, 90));
```

- anonymous function(無名関数)

```js
let bmi: (height: number, weight: number) => number = function (
  height: number,
  weight: number
): number {
  return weight / (height * height);
};
console.log(bmi(1.78, 86));
```

- arrow function

```js
let bmi: (height: number, weight: number) => number = (
  height: number,
  weight: number
): number => weight / (height * height);
console.log(bmi(1.78, 86));
```

- optional arguments ... ? を付与することで任意の引数とすることができる

```js
let bmi: (height: number, weight: number, printable?: boolean) => number = (
  height: number,
  weight: number,
  printable?: boolean
): number => {
  const bmi = weight / (height * height);
  if (printable) {
    console.log({ bmi });
  }
  return bmi;
};
// bmi(身長, 体重, console.logで出力するかどうか?)
bmi(1.78, 86, true);
bmi(1.78, 86, false);
bmi(1.78, 86);
```

- default parameters

```js
const nextYearSalary = (currentSalary: number, rate: number = 1.1) =>
  currentSalary * rate;
console.log(nextYearSalary(1000, 1.05));
console.log(nextYearSalary(1000));
```

- rest parameters

```js
const reducer = (accumulator: number, currentValue: number) => {
  console.log({ accumulator, currentValue });
  return accumulator + currentValue;
};

const sum: (...values: number[]) => number = (...values: number[]): number => {
  return values.reduce(reducer);
};
console.log(sum(1, 2, 3, 4, 5));
```

- overload

```js
// シグネチャの宣言
function double(value: number): number;
function double(value: string): string;

// 実体の記述
function double(value: any): any {
  if (typeof value === 'number') {
    return value * 2;
  } else {
    return value + value;
  }
}
console.log(double(100));
console.log(double('Go '));
```

# クラスで型を使う

- class

```js
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  profile(): string {
    return `name: ${this.name}, age: ${this.age}`;
  }
}
let taro = new Person('taro', 30);
console.log(taro);
console.log(taro.profile());
```

- アクセス修飾子(スコープ)

```js
class Person {
  name: string;
  // private age: number;
  protected age: number;
  protected nationality: string;

  constructor(name: string, age: number, nationality: string) {
    this.name = name;
    this.age = age;
    this.nationality = nationality;
  }

  profile(): string {
    return `name: ${this.name}, age: ${this.age}`;
  }
}
class Android extends Person {
  constructor(name: string, age: number, nationality: string) {
    super(name, age, nationality);
  }

  profile(): string {
    return `name: ${this.name}, age: ${this.age}, nationality: ${this.nationality}`;
  }
}
let taro = new Person('Taro', 30, 'Japan');
console.log(taro.name);
// console.log(taro.age);
console.log(taro.profile());
```

- constructor  
  コンストラクタで変数宣言がついでにできちゃう

```js
class Person {
  constructor(public name: string, protected age: number) {}
}
const me = new Person('Ham', 43);
console.log(me);
```

- getter / setter

```js
// * owner
//   * 初期化時に設定できる。
//   * 途中で変更できない。
//   * 参照できる。
// * secretNumber
//   * 初期化時に設定できる。
//   * 途中で変更できる。
//   * 参照できない。
class MyNumberCard {
  constructor(private _owner: string, private _secretNumber: number) {}

  get owner() {
    return this._owner;
  }

  set secretNumber(value: number) {
    this._secretNumber = value;
  }
  get secretNumber() {
    return this._secretNumber;
  }
}
let card = new MyNumberCard('Ham', 1234567890);
card.secretNumber = 1111111111;
console.log(card.secretNumber);
```

- readonly

```js
class VisaCard {
  constructor(public readonly owner: string) {}
}
let myVisaCard = new VisaCard('Ham');
console.log(myVisaCard.owner);
// myVisaCard.owner = 'はむ'; // Error!!
```

- 静的メンバ

```js
class Me {
  static isProgrammer: boolean = true;
  static firstName: string = 'Atsushi';
  static lastName: string = 'Ishida';

  static work() {
    return `Hey, guys! This is ${this.firstName}! Are you intersted in TypeScript? Lets dive into TypeScript!`;
  }
}
console.log(Me.isProgrammer);
console.log(Me.work());
```

- namespace(名前空間)

```js
namespace Japanese {
  export namespace Tokyo {
    export class Person {
      constructor(public name: string) {}
    }
  }
  export namespace Osaka {
    export class Person {
      constructor(public name: string) {}
    }
  }
}
namespace English {
  class Person {
    constructor(
      public firstName: string,
      public middleName: string,
      public lastName: string
    ) {}
  }
}
const me = new Japanese.Tokyo.Person('Ham');
console.log(me.name);
// const me2 = new English.Person('Ham'); // Error!! exportしないと外部から参照できない
```

- inheritance(継承)

```js
class Animal {
  constructor(public name: string) {}
  run(): string {
    return `I can run `;
  }
}
class Lion extends Animal {
  public speed: number;
  constructor(name: string, speed: number) {
    super(name);
    this.speed = speed;
  }
  run(): string {
    const parentMessage = super.run();
    return `${parentMessage}${this.speed}km/h`;
  }
}
// console.log(new Animal('Mickey').run());
console.log(new Lion('Shimba', 80).run());
```

- 抽象クラス / 抽象メソッド

```js
// 抽象クラス
abstract class Animal {
  abstract cry(): string;
}

class Lion extends Animal {
  cry() {
    return 'roar';
  }
}
// class Tiger extends Animal {}  // Error!! 抽象クラスを継承した場合、メソッドを実装しなければならない
```

- Interface

```js
class Mahotsukai {}
class Souryo {}
// class Taro extends Mahotsukai, Souryo {} // Error!! 多重継承はエラーになる

// インターフェース
interface Kenja {
  ionazun(): void;
}
interface Senshi {
  kougeki(): void;
}
// インターフェースなら複数クラスを継承できる（正確には実装するという）
class Jiro implements Kenja, Senshi {
  ionazun(): void {
    console.log('ionazun');
  }
  kougeki(): void {
    console.log('kougeki');
  }
}
const jiro = new Jiro();
jiro.ionazun();
jiro.kougeki();
```

- 総称型(ジェネリクス)

```js
// <T>は抽象的な型(stirngも入るしnumberも入る)
// 慣例的に<T>と記述される
const echo = <T>(arg: T): T => {
  return arg;
};
console.log(echo<number>(100));
console.log(echo<string>('Hello'));
console.log(echo<boolean>(true));

class Mirror<T> {
  constructor(public value: T) {}
  echo(): T {
    return this.value;
  }
}
console.log(new Mirror<number>(123).echo());
console.log(new Mirror<string>('Hello, generics').echo());
```

- 型アサーション

```js
let name: any = 'Ham';

// 型アサーション
let length1: number = name.length;
let length2 = name.length as number;
let length3 = (name as string).length;
let length4 = (<string>name).length; // 非推奨(JSXと相性が悪いため)
```

- const アサーション

```js
let name = 'Atsushi';
let nickName = 'Ham' as const;
let profile = {
  name: 'Atsushi',
  height: 178,
} as const;
```

- Nullable Types

```js
let profile: { name: string, age: number | null } = {
  name: 'Ham',
  age: null,
};
// コンパイルオプションを変更することでnullも代入可能になる=>これをヌーラブルな状態という
// tsconfig.json
// "strictNullChecks": true →　false
// ただし、これは全体に適用されてしまうため、非推奨
```

- インデックスシグネチャ

# 【Tips】ライブラリ

- [axios](https://github.com/axios/axios) ... 外部 API と通信するためのライブラリ

```bash
$ npm info axios
axios@0.19.2 | MIT | deps: 1 | versions: 42

$ npm install axios@0.19.2
```
