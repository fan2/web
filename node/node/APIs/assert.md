"Deep" equality means that the enumerable "own" properties of child objects are evaluated also:

```shell
faner@MBP-FAN:~|⇒  node
> const assert = require('assert')
undefined

> const assert = require('assert');
SyntaxError: Identifier 'assert' has already been declared
> assert(true)
undefined
> assert(false)
AssertionError [ERR_ASSERTION]: false == true
> let a = 5
undefined
> let b = '10'
undefined
> let c = 10
undefined
> assert.equal(a, b)
AssertionError [ERR_ASSERTION]: 5 == '10'
> assert.equal(b, c)
undefined
> assert.strictEqual(b, c)
AssertionError [ERR_ASSERTION]: Input A expected to strictly equal input B:
+ expected - actual

- '10'
+ 10
> assert.deepStrictEqual({ a: 1 }, { a: '1' });
AssertionError [ERR_ASSERTION]: Input A expected to strictly deep-equal input B:
+ expected - actual

  {
-   a: 1
+   a: '1'
  }

> assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
undefined
> assert.deepStrictEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
AssertionError [ERR_ASSERTION]: Input A expected to strictly deep-equal input B:
+ expected - actual ... Lines skipped

  [
    [
...
        2,
-       3
+       '3'
      ]
...
    5
  ]
>
```
