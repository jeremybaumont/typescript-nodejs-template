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


