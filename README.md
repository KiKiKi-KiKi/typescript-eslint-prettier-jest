# TypeScript + ESLint + Prettier + Jest

## TypeScript

```sh
$ npm i --save-dev typescript
npx tsc --init
```

`tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "es5", /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', 'ES2021', or 'ESNEXT'. */
    "module": "commonjs", /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    "lib": ["dom", "dom.iterable", "ES2017"], /* Specify library files to be included in the compilation. */
    "declaration": true /* Generates corresponding '.d.ts' file. */,
    "sourceMap": true, /* Generates corresponding '.map' file. */
    "outDir": "./dist", /* Redirect output structure to the directory. */
    "downlevelIteration": true, /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    "strict": true, /* Enable all strict type-checking options. */
    "noImplicitThis": true, /* Raise error on 'this' expressions with an implied 'any' type. */
    "noUnusedLocals": true, /* Report errors on unused locals. */
    "noUnusedParameters": true, /* Report errors on unused parameters. */
    "noImplicitReturns": true, /* Report error when not all code paths in function return a value. */
    "esModuleInterop": true, /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    "experimentalDecorators": true, /* Enables experimental support for ES7 decorators. */
    "emitDecoratorMetadata": true, /* Enables experimental support for emitting type metadata for decorators. */
    "skipLibCheck": true, /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true /* Disallow inconsistently-cased references to the same file. */
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

## ESLint

```sh
$ npm i --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

### setting

```sh
$ npx eslint --init
? How would you like to use ESLint?
❯ To check syntax, find problems, and enforce code style
? What type of modules does your project use?
❯ JavaScript modules (import/export)
? Which framework does your project use?
❯ None of these
? Does your project use TypeScript? Yes
? Where does your code run?
✔ Browser
? How would you like to define a style for your project?
❯ Use a popular style guide
? Which style guide do you want to follow? … 
❯ Airbnb: https://github.com/airbnb/javascript
? What format do you want your config file to be in? … 
❯ JavaScript
```

### ESLint with TypeScript

`.eslintrc.js`
```js
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'airbnb-base',
    'plugin:@typescript-eslint/recommended',
    'plugin:@typescript-eslint/recommended-requiring-type-checking',
  ],
  plugins: ['@typescript-eslint'],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    // cf. https://github.com/typescript-eslint/typescript-eslint/releases/tag/v2.0.0
    project: './tsconfig.json',
    sourceType: 'module',
  },
  settings: {
    'import/extensions': ['.js', '.jsx', '.ts', '.tsx'],
    'import/parsers': {
      '@typescript-eslint/parser': ['.ts', '.tsx'],
    },
    'import/resolver': {
      node: {
        extensions: ['.js', '.jsx', '.ts', '.tsx'],
      },
    },
  },
  rules: {
    // Allow import without extensions
    'import/extensions': [
      'error',
      'ignorePackages',
      { js: 'never', jsx: 'never', ts: 'never', tsx: 'never' },
    ],
    // Allow named export
    'import/prefer-default-export': 'off',
    'newline-before-return': 'error',
    'no-console': 'warn',
    'no-var': 'error',
  },
};

```

### Ignore `.eslintrc.js` from ESLint project target

FIX VSCode Error of `Parsing error: "parserOptions.project" has been set for @typescript-eslint/parser. The file does not match your project config: .eslintrc.js. The file must be included in at least one of the projects provided.`

```sh
$ echo '/.eslintrc.js' >> .eslintignore
```
