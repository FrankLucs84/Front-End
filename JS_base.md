# 📘 JavaScript Cheatsheet - Regole e Particolarità

## 🔹 Dichiarazione Variabili
```js
var x = 1;        // Function scope, riassegnabile, può creare bug
let x = 2;        // Block scope, riassegnabile
const x = 3;      // Block scope, non riassegnabile
```

## 🔹 Tipi di Dati
```js
// Primitivi
string, number, boolean, null, undefined, symbol, bigint

// Oggetti
Object, Array, Function, Date, RegExp, ecc.
```

## 🔹 Coercizione di Tipo
```js
'5' + 1    // "51"
'5' - 1    // 4
true + 1   // 2
false == 0 // true
false === 0 // false
```

## 🔹 Funzioni
```js
function classic(a, b) {
  return a + b;
}

const arrow = (a, b) => a + b; // non ha proprio "this"
```

## 🔹 Scope e Hoisting
```js
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 10;
```

## 🔹 Oggetti e Array
```js
const obj = {name: "Anna"};
const arr = [1, 2, 3];

obj.name = "Luca"; // modificabile
arr.push(4);       // modificabile
```

## 🔹 Destructuring
```js
const {name} = obj;
const [first, second] = arr;
```

## 🔹 Spread & Rest
```js
const newArr = [...arr, 4];
function sum(...args) { return args.reduce((a,b)=>a+b); }
```

## 🔹 Optional Chaining & Nullish
```js
obj?.prop?.subProp;     // undefined se non esiste
let x = val ?? 'default'; // solo se null o undefined
```

## 🔹 Asincronia
```js
async function getData() {
  const res = await fetch('...');
  const data = await res.json();
}
```

## 🔹 Promesse
```js
fetch(url)
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

## 🔹 Classi
```js
class Persona {
  constructor(nome) {
    this.nome = nome;
  }
  saluta() {
    console.log(`Ciao ${this.nome}`);
  }
}
```

## 🔹 Moduli (ES Modules)
```js
// file.js
export const x = 1;
export default function saluta() {...}

// main.js
import saluta, { x } from './file.js';
```

## 🔹 Altri tips particolari
- `==` fa coercizione, `===` è rigoroso.
- `NaN !== NaN`, usa `Number.isNaN()`
- `typeof null === 'object'` (bug storico)
- Oggetti con chiavi duplicate: l’ultima vince.
- `setTimeout(fn, 0)` non esegue subito: finisce lo stack prima.
