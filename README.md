# Basic ESLint eslint.config.js file

```javascript
import globals from 'globals';
import pluginJs from '@eslint/js';
import jestPlugin from 'eslint-plugin-jest';
import nodePlugin from 'eslint-plugin-node';
import pluginPromise from 'eslint-plugin-promise';
import pluginSecurity from 'eslint-plugin-security';

export default [
    {
        // Define global variables for Node.js and Jest to avoid ESLint errors
        languageOptions: {
            globals: {
                ...globals.node, // Includes global Node.js variables (e.g., `__dirname`, `process`)
                ...globals.jest  // Includes Jest testing framework globals (e.g., `describe`, `it`, `expect`)
            }
        }
    },
    
    // Register plugins for Jest and Node.js rules
    { 
        plugins: { 
            jest: jestPlugin,  // Enables Jest-specific linting rules
            node: nodePlugin   // Enables Node.js-specific linting rules
        } 
    },
    
    {
        rules: {
            // **Code Style Rules**
            
            // Enforce the use of single quotes, but allow double quotes if escaping is needed
            'quotes': ['error', 'single', { 'avoidEscape': true, 'allowTemplateLiterals': true }], 
            
            // Require semicolons at the end of statements
            'semi': ['error', 'always'], 
            
            // Enforce consistent indentation of 4 spaces per level
            'indent': ['error', 4], 
            
            // Disallow trailing commas at the end of object and array literals
            'comma-dangle': ['error', 'never'], 
            
            // Warn if a line exceeds 100 characters (excluding comments)
            'max-len': ['warn', { 'code': 100, 'ignoreComments': true }], 
            
            // Allow only `console.warn` and `console.error`, but warn on `console.log`
            'no-console': ['warn', { 'allow': ['warn', 'error'] }], 

            // **Best Practices**
            
            // Require strict equality (`===` and `!==`) instead of loose equality (`==` and `!=`)
            'eqeqeq': ['error', 'always'], 
            
            // Enforce curly braces for all control statements (e.g., `if`, `for`, `while`)
            'curly': ['error', 'all'], 
            
            // Disallow usage of `var`; prefer `let` and `const`
            'no-var': 'error', 
            
            // Require `const` if a variable is never reassigned
            'prefer-const': 'error', 
            
            // Warn if there are unused variables, but allow variables prefixed with `_` (e.g., `_unused`)
            'no-unused-vars': ['warn', { 'argsIgnorePattern': '^_' }], 
            
            // Disallow multiple consecutive empty lines (allow a maximum of one)
            'no-multiple-empty-lines': ['error', { 'max': 1 }], 

            // **Node.js-Specific Rules**
            
            // Allow requiring modules that are not in `package.json` (useful for dev dependencies)
            'node/no-unpublished-require': 'off', 
            
            // Allow missing imports for ES module compatibility
            'node/no-missing-import': 'off', 
            
            // Disallow `process.exit()` to prevent premature application exits
            'node/no-process-exit': 'error', 

            // **Promise Handling Rules**
            
            // Require returning a value inside a `.then()` handler in Promises
            'promise/always-return': 'error', 
            
            // Ensure that errors in Promises are caught with `.catch()` or `try/catch`
            'promise/catch-or-return': 'error', 
            
            // Disallow unnecessary wrapping of values in `Promise.resolve()` or `Promise.reject()`
            'promise/no-return-wrap': 'error', 

            // **Security Best Practices**
            
            // Warn about object property injection attacks (e.g., `user[input] = value;`)
            'security/detect-object-injection': 'warn', 
            
            // Warn when using non-literal filenames in `fs` functions (e.g., `fs.readFile(userInput)`)
            'security/detect-non-literal-fs-filename': 'warn', 

            // **Performance Rules**
            
            // Disallow `async` functions as `Promise` executors to avoid unexpected behavior
            'no-async-promise-executor': 'error', 
            
            // Disallow `async` functions without an `await` inside them
            'require-await': 'error', 
            
            // Disallow redundant `return await` inside async functions
            'no-return-await': 'error' 
        }
    },

    // Extend ESLint's recommended JavaScript rules
    pluginJs.configs.recommended,

    // Extend recommended rules for handling Promises correctly
    pluginPromise.configs['flat/recommended'],

    // Extend security-related rules to prevent common security issues
    pluginSecurity.configs.recommended
];
```

## Dependencies
```
npm install --save-dev \
@eslint/js@^9.28.0 \
@eslint/json@^0.12.0 \
eslint@^9.28.0 \
eslint-plugin-node@^11.1.0 \
eslint-plugin-promise@^7.2.1 \
eslint-plugin-security@^3.0.1 \
globals@^16.2.0
```
