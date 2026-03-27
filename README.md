<div align="center">
  <img src="https://raw.githubusercontent.com/igorskyflyer/npm-oxlint-config/main/media/oxlint-config.png" alt="Icon of Oxlint Config" width="256" height="256">
  <h1>Oxlint Config</h1>
</div>

<blockquote align="center">oxlint Powered • 7 Plugins • 80+ Rules • Zero Bikeshedding</blockquote>

<h4 align="center">
  ⚓ Strict, no-nonsense oxlint rules that catch real bugs and enforce clean code. 🐳
</h4>

<br>

## Table of Contents

- ✨ [**Features**](#features)
- 🕵🏼 [**Usage**](#usage)
- ⚙️ [**Implementation**](#implementation)
- 🎯 [**Motivation**](#motivation)
- 📝 [**Changelog**](#changelog)
- 🪪 [**License**](#license)
- 💖 [**Support**](#support)
- 🧬 [**Related**](#related)
- 👨🏻‍💻 [**Author**](#author)

<br>

## Features

- ⚓ Strict, opinionated oxlint config for modern `JavaScript` and `TypeScript` projects
- 🔍 Catches unused variables, imports, explicit `any`, floating promises and unsafe assignments
- 📦 Covers `typescript`, `import`, `node`, `promise`, `unicorn`, `jest` and `vitest` plugins
- 🚀 `node:` protocol enforced, barrel files flagged, accumulating spreads detected
- 🔄 Import cycle, duplicate and absolute path detection built-in
- 🧪 Vitest-aware rules - no focused, disabled or conditionally skipped tests slip through
- 🦄 Unicorn rules for modern idioms - `prefer-at`, `prefer-includes`, `numeric-separators` and more
- 🛡️ Zero bikeshedding - one config, all projects, extend and go

<br>

## Usage

Install it by executing any of the following, depending on the preferred package manager:

```bash
pnpm add -D @igorskyflyer/oxlint-config
```

```bash
yarn add -D @igorskyflyer/oxlint-config
```

```bash
npm i -D @igorskyflyer/oxlint-config
```

<br>

Then extend the config in `.oxlintrc.json`:

```json
{
  "extends": ["@igorskyflyer/oxlint-config"]
}
```

Override any rule locally as needed:

```json
{
  "extends": ["@igorskyflyer/oxlint-config"],
  "rules": {
    "no-console": "error"
  }
}
```

<br>

## Implementation

### Options

- **`typeAware: false`** - disabled by default - requires the `oxlint-tsgolint` peer dependency, enable locally when available for deeper type-aware analysis
- **`denyWarnings: false`** - warnings do not produce a non-zero exit code, keeping CI pipelines unblocked for non-critical issues
- **`reportUnusedDisableDirectives: "warn"`** - flags stale `// oxlint-disable` comments that no longer suppress anything

### Plugins

- **`typescript`** - type safety, imports, class members and unsafe assignment detection
- **`import`** - clean import hygiene - no duplicates, no cycles, no absolute paths
- **`node`** - Node.js-specific rules including `node:` protocol enforcement
- **`promise`** - catches common Promise misuse patterns and anti-patterns
- **`unicorn`** - modern idioms - `prefer-at`, `prefer-includes`, numeric separators and more
- **`jest`** - shared test rules used by both Jest and Vitest in oxlint
- **`vitest`** - Vitest-specific rules on top of the jest plugin

### Rules

**General:**

- **`no-console: "warn"`** - console statements are development artifacts, not production code
- **`no-undef: "error"`** - referencing undefined variables is always a bug
- **`no-unused-vars: "error"`** - unused variables are dead code and signal incomplete refactors
- **`no-unused-expressions: "error"`** - expressions with no effect are always a bug or dead code
- **`no-unused-private-class-members: "error"`** - unused private members are dead code
- **`no-shadow: "warn"`** - shadowed variables cause subtle, hard-to-spot bugs
- **`no-await-in-loop: "warn"`** - awaiting in loops is almost always a performance mistake
- **`no-constructor-return: "error"`** - returning from a constructor is always wrong
- **`no-promise-executor-return: "error"`** - returning from a Promise executor is a bug
- **`no-self-compare: "error"`** - comparing a value to itself is always a bug
- **`no-template-curly-in-string: "warn"`** - `"${var}"` instead of `` `${var}` `` is a common typo
- **`no-new: "warn"`** - using `new` purely for side effects is suspicious
- **`no-extend-native: "error"`** - extending native prototypes breaks the ecosystem
- **`no-new-wrappers: "error"`** - `new String()` and friends are never correct
- **`no-proto: "error"`** - `__proto__` is deprecated, use `Object.getPrototypeOf()` instead
- **`no-var: "error"`** - `var` is obsolete, use `const` or `let`
- **`no-eval: "error"`** - `eval` is a security vulnerability
- **`no-implied-eval: "error"`** - `setTimeout("code")` is `eval` in disguise
- **`prefer-const: "error"`** - prefer immutability by default
- **`eqeqeq: "error"`** - always use strict equality
- **`require-await: "error"`** - async functions without `await` are misleading
- **`require-yield: "error"`** - generators without `yield` are pointless

**TypeScript:**

- **`typescript/no-explicit-any: "error"`** - `any` defeats the purpose of TypeScript entirely
- **`typescript/no-inferrable-types: "off"`** - explicit types on inferrable values are allowed, clarity over brevity
- **`typescript/consistent-type-imports: "error"`** - enforces `import type` for type-only imports, reduces runtime overhead
- **`typescript/consistent-generic-constructors: "error"`** - consistent placement of generic type annotations
- **`typescript/adjacent-overload-signatures: "error"`** - overload signatures must be grouped together for readability
- **`typescript/no-misused-promises: "error"`** - passing async functions where sync is expected causes subtle bugs
- **`typescript/no-floating-promises: "error"`** - unhandled promises are silent failures
- **`typescript/no-unnecessary-type-assertion: "warn"`** - redundant type assertions add noise
- **`typescript/no-unnecessary-boolean-literal-compare: "warn"`** - `x === true` is redundant
- **`typescript/no-unsafe-assignment: "error"`** - prevents `any` from silently spreading through the codebase
- **`typescript/no-unsafe-call: "error"`** - calling `any` typed values is unsafe
- **`typescript/no-unsafe-member-access: "error"`** - accessing members of `any` typed values is unsafe
- **`typescript/no-unsafe-return: "error"`** - returning `any` typed values pollutes callers
- **`typescript/await-thenable: "error"`** - awaiting non-thenables is always a bug
- **`typescript/no-for-in-array: "error"`** - `for...in` on arrays produces unexpected results
- **`typescript/prefer-nullish-coalescing: "warn"`** - `??` is safer than `||` for nullish checks
- **`typescript/prefer-includes: "error"`** - `indexOf >= 0` should be `includes()`
- **`typescript/return-await: "error"`** - returning a promise inside try/catch requires `await`
- **`typescript/only-throw-error: "error"`** - only `Error` objects should be thrown
- **`typescript/ban-ts-comment: "warn"`** - `@ts-ignore` silences errors instead of fixing them
- **`typescript/switch-exhaustiveness-check: "warn"`** - missing switch cases on union types are likely bugs
- **`typescript/no-array-delete: "error"`** - deleting array elements leaves holes
- **`typescript/no-base-to-string: "error"`** - calling `.toString()` on objects that return `[object Object]`
- **`typescript/no-duplicate-type-constituents: "error"`** - duplicate types in unions/intersections are noise
- **`typescript/no-redundant-type-constituents: "error"`** - redundant type members simplify nothing
- **`typescript/no-wrapper-object-types: "error"`** - `String`, `Number`, `Boolean` as types are wrong
- **`typescript/prefer-as-const: "error"`** - use `as const` instead of literal type assertions
- **`typescript/restrict-template-expressions: "error"`** - prevents unsafe values in template literals
- **`typescript/no-misused-spread: "error"`** - spreading non-iterable values causes runtime errors

**Import:**

- **`import/no-duplicates: "error"`** - duplicate imports from the same module are redundant
- **`import/no-self-import: "error"`** - a module importing itself is always a mistake
- **`import/no-cycle: "warn"`** - circular imports cause hard-to-debug runtime issues
- **`import/no-named-as-default: "warn"`** - importing a named export as default is likely a mistake
- **`import/no-absolute-path: "error"`** - absolute imports break portability across environments
- **`import/no-empty-named-blocks: "error"`** - `import {} from 'x'` is completely pointless

**Node:**

- **`node/no-new-require: "error"`** - `new require()` is never correct
- **`node/no-path-concat: "error"`** - use `path.join()` instead of string concatenation for paths
- **`node/no-process-env: "warn"`** - direct `process.env` access should be centralized

**Unicorn:**

- **`unicorn/prefer-node-protocol: "error"`** - always use `node:` prefix for built-ins
- **`unicorn/no-useless-promise-resolve-reject: "error"`** - wrapping in `Promise.resolve/reject` inside async is redundant
- **`unicorn/no-unnecessary-await: "error"`** - awaiting a non-promise is pointless
- **`unicorn/prefer-string-starts-ends-with: "error"`** - cleaner than `indexOf` or `slice` checks
- **`unicorn/error-message: "error"`** - errors must always have a message
- **`unicorn/no-instanceof-array: "error"`** - use `Array.isArray()` instead
- **`unicorn/throw-new-error: "error"`** - always use `new` when throwing errors
- **`unicorn/prefer-includes: "error"`** - `indexOf >= 0` should be `includes()`
- **`unicorn/no-array-for-each: "warn"`** - prefer `for...of` over `.forEach()`
- **`unicorn/prefer-at: "error"`** - `arr[arr.length - 1]` should be `arr.at(-1)`
- **`unicorn/no-typeof-undefined: "error"`** - `typeof x === 'undefined'` should be `x === undefined`
- **`unicorn/prefer-string-slice: "error"`** - `substr`/`substring` are deprecated, use `slice`
- **`unicorn/no-useless-undefined: "error"`** - explicit `return undefined` is implicit
- **`unicorn/no-nested-ternary: "error"`** - nested ternaries are unreadable
- **`unicorn/prefer-ternary: "off"`** - prefer using `if/else` for readability
- **`unicorn/numeric-separators-style: "error"`** - `1000000` should be `1_000_000`
- **`unicorn/prefer-date-now: "error"`** - `new Date().getTime()` should be `Date.now()`
- **`unicorn/no-static-only-class: "error"`** - use a plain object instead of a static-only class
- **`unicorn/no-array-reduce: "warn"`** - `reduce` is often harder to read than a loop
- **`unicorn/no-single-promise-in-promise-methods: "error"`** - `Promise.all([x])` should just be `await x`
- **`unicorn/no-useless-fallback-in-spread: "error"`** - `[...(x || [])]` is redundant when `x` is always iterable
- **`unicorn/prefer-string-replace-all: "error"`** - use `replaceAll` instead of `replace` with a global regex
- **`unicorn/prefer-array-flat-map: "error"`** - `.map().flat()` should be `.flatMap()`
- **`unicorn/no-empty-file: "error"`** - empty files are always dead code
- **`unicorn/no-thenable: "error"`** - objects with `.then()` are accidentally treated as promises
- **`unicorn/prefer-set-size: "error"`** - use `set.size` instead of `[...set].length`
- **`unicorn/prefer-set-has: "warn"`** - `Set.has()` is O(1) vs `Array.includes()` O(n)
- **`unicorn/no-await-in-promise-methods: "error"`** - `Promise.all([await x])` defeats the purpose
- **`unicorn/custom-error-definition": "error": "error"`** - enforces the only valid way of `Error` subclassing

**OXC:**

- **`oxc/bad-array-method-on-arguments: "error"`** - `arguments` is not a real array
- **`oxc/bad-comparison-sequence: "error"`** - `a < b < c` does not work as expected
- **`oxc/missing-throw: "error"`** - `new Error()` without `throw` is always a bug
- **`oxc/no-accumulating-spread: "warn"`** - spreading inside a loop has O(n²) complexity
- **`oxc/no-barrel-file: "warn"`** - barrel files hurt tree-shaking and build performance
- **`oxc/double-comparisons: "error"`** - redundant double comparisons
- **`oxc/bad-min-max-func: "error"`** - incorrect use of `Math.min`/`Math.max`
- **`oxc/bad-object-literal-comparison: "error"`** - comparing object literals is always `false`
- **`oxc/const-comparisons: "error"`** - comparisons that are always true or false
- **`oxc/erasing-op: "error"`** - operations that always erase their operand
- **`oxc/only-used-in-recursion: "warn"`** - parameters only used in recursion can be simplified

**Promise:**

- **`promise/no-return-wrap: "error"`** - wrapping in `Promise.resolve()` inside async is redundant
- **`promise/param-names: "error"`** - Promise constructor params must be named `resolve` and `reject`
- **`promise/no-multiple-resolved: "error"`** - resolving or rejecting a Promise more than once is a bug
- **`promise/valid-params: "error"`** - Promise methods must receive the correct number of arguments
- **`promise/no-callback-in-promise: "warn"`** - using callbacks inside Promise chains causes unpredictable behavior
- **`promise/no-nesting: "warn"`** - nested `.then()` chains should use `async/await`
- **`promise/no-promise-in-callback: "warn"`** - using Promises inside callbacks causes unpredictable behavior

**Jest/Vitest:**

- **`jest/no-disabled-tests: "warn"`** - disabled tests are technical debt
- **`jest/no-focused-tests: "error"`** - `test.only` must never reach production CI
- **`jest/consistent-test-it: "error"`** - enforces consistent use of `test` or `it`
- **`jest/no-identical-title: "error"`** - duplicate test titles make failures impossible to distinguish
- **`jest/valid-title: "error"`** - test titles must be valid and meaningful
- **`jest/valid-expect: "error"`** - `expect()` must be called correctly
- **`jest/no-conditional-expect: "error"`** - conditional expects hide test failures
- **`jest/no-standalone-expect: "error"`** - `expect()` outside a test block is always a bug
- **`jest/require-to-throw-message: "error"`** - `toThrow()` without a message is too broad
- **`jest/valid-describe-callback: "error"`** - describe callbacks must be valid functions
- **`vitest/no-conditional-tests: "error"`** - conditional tests hide failures
- **`vitest/hoisted-apis-on-top: "warn"`** - `vi.mock()` and similar must be hoisted
- **`vitest/warn-todo: "warn"`** - todo tests signal unfinished work
- **`vitest/consistent-each-for: "error"`** - consistent use of `each` for parameterized tests
- **`vitest/prefer-strict-boolean-matchers: "error"`** - enforce using `toBe(true)` and `toBe(false)` over matchers that coerce types to boolean

<br>

## Motivation

Every project deserves consistent, battle-tested linting from day one - not a config assembled from memory, copy-pasted from a previous project or missing half the plugins.

`@igorskyflyer/oxlint-config` provides a single, versioned, opinionated baseline covering seven plugin ecosystems. Drop it in, extend if needed, and focus on the actual code.

<br>

## Changelog

Read about the latest changes in the [**CHANGELOG**](https://github.com/igorskyflyer/npm-oxlint-config/blob/main/CHANGELOG.md).

<br>

## License

Licensed under the [**MIT license**](https://github.com/igorskyflyer/npm-oxlint-config/blob/main/LICENSE).

<br>

## Support

<div align="center">
  Engineering and documenting open-source projects<br>
  involves a significant investment of time.
  <br><br>
  If this project or its implementation has provided value,<br>
  support is greatly appreciated.
  <br><br>
  <a href="https://ko-fi.com/igorskyflyer" target="_blank"><img src="https://raw.githubusercontent.com/igorskyflyer/igorskyflyer/main/assets/ko-fi.png" alt="Donate to igorskyflyer" width="180" height="46"></a>
  <br><br>
  <em>Thank you for supporting these efforts!</em> 🙏😊
</div>

<br>

## Related

[**@igorskyflyer/astro-render-component**](https://www.npmjs.com/package/@igorskyflyer/astro-render-component)

> _🤖 Astro component renderer. Zero configuration. Produces clean HTML strings directly in Node.js without any DOM environment. 🐬_

<br>

[**@igorskyflyer/adblock-filter-counter**](https://www.npmjs.com/package/@igorskyflyer/adblock-filter-counter)

> _🐲 A lightweight npm module for counting ad-block filter rules, ultra-simple, fast, and perfect for list maintainers, filter testers, and privacy tool developers.🦘_

<br>

[**@igorskyflyer/zep**](https://www.npmjs.com/package/@igorskyflyer/zep)

> _🧠 Zep is a zero-dependency, efficient debounce module. ⏰_

<br>

[**@igorskyflyer/magic-string**](https://www.npmjs.com/package/@igorskyflyer/magic-string)

> _🧵 An expressive and chainable library for advanced string manipulations. Supports appending, prepending, trimming, quoting, and path formatting with customizable whitespace handling. Makes advanced String manipulations a piece of cake. 🦥_

<br>

[**@igorskyflyer/valid-path**](https://www.npmjs.com/package/@igorskyflyer/valid-path)

> _🧰 Determines whether a given value can be a valid file/directory name. 🏜_

<br>

## Author

Created by **Igor Dimitrijević ([_@igorskyflyer_](https://github.com/igorskyflyer/))**.
