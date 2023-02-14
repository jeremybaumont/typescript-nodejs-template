# README


* Setup the version of Node.js  by setting up a `.nvmrc` file.
```
nvm use stable
node -v > .nvmrc
```

* Initialise npm configuration `package.json`.
```
npm init -y
```

* Allow import/export of ESM module by adding the "type" field in the 
`package.json` set to "module".

A `package.json` "type" value of "module" tells Node.js to interpret .js files 
within that package as using ES module syntax.


This setting controls whether .js files are interpreted as ES modules or CommonJS 
modules, and defaults to CommonJS when not set. When a file is considered an 
ES module, a few different rules come into play compared to CommonJS:

** import/export statements can be used.
** Top-level await can be used
** Relative import paths need full extensions (we have to write import "./foo.js" instead of import "./foo").
** Imports might resolve differently from dependencies in node_modules.
** Certain global-like values like require and module cannot be used directly.
** CommonJS modules get imported under certain special rules.

Now, we can create an `index.js` file that uses the import.
```
import fs from 'fs';
```
And we don't get any error:
```
> node index.js
(node:19620) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.
(Use `node --trace-warnings ...` to show where the warning was created)
/home/jmb/code/learn/typescript/typesprict-nodejs/index.js:1
import fs from 'fs';
^^^^^^

SyntaxError: Cannot use import statement outside a module
    at internalCompileFunction (node:internal/vm:73:18)
    at wrapSafe (node:internal/modules/cjs/loader:1166:20)
    at Module._compile (node:internal/modules/cjs/loader:1210:27)
    at Module._extensions..js (node:internal/modules/cjs/loader:1300:10)
    at Module.load (node:internal/modules/cjs/loader:1103:32)
    at Module._load (node:internal/modules/cjs/loader:942:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:83:12)
    at node:internal/main/run_main_module:23:47

Node.js v19.6.0
```

* Install TypeScript npm package.
```
npm install typescript --save-dev
```

* Add npm run scripts to build TypeScript.
```
"scripts": {
    "build": "tsc",
    ...
}
```

* Create `src` directory and move `index.ts` file into.

* Install TypeScript Node.js types.
```
npm i -D @types/node
```
This will avoid compilation error or IDE warning complaining about TypeScript,
that cannot find the types.
```
> tsc src/index.ts 

> typesprict-nodejs@1.0.0 build
> tsc

src/index.ts:1:16 - error TS2307: Cannot find module 'fs' or its corresponding type declarations.

1 import fs from 'fs';
                 ~~~~


Found 1 error in src/index.ts:1
```

* Add TypeScript configuratoin `tsconfig.json`.
```
{
    "compilerOptions": {
        "module": "nodenext",
        "moduleResolution": "nodenext",
        "target": "ES2020",
        "sourceMap": true,
        "outDir": "dist"
    },
    "include": ["src/**/**"]
}
```

"module" sets to "nodenext" integrate with Node’s native ECMAScript Module support. 
The emitted JavaScript uses ES2020 output depending on the file extension 
and the value of the type setting in the nearest package.json.
[change-log TypeScript 4.7](https://devblogs.microsoft.com/typescript/announcing-typescript-4-7/#esm-nodejs)

