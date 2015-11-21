# QUnit Roadmap

QUnit is following a strict semantic versioning, where:

from a `major.minor.patch` model:

- every breaking changes should be addressed at major versions.
- every new features should be addressed at minor versions.
- releases with only bug fixes or internal build improvements should be addresed as patches.

That means:

- a patch will never introduce a new feature.
- a minor version will never be released for only bug fixes.
- patches and minor versions will not break any public API feature.
- major version will not introduce any new feature

This was the same approach from Ember 1.x to Ember 2, and it worked flawlessly for most people.

There is a minor trade off, development is gonna be hard. We should care about who is using and prioritize our work on any regressions.

Every new introduced feature requires a lot of discussion and good arguments, regrets are not welcome.

Ref: https://t.co/5vBoIl01K6

---

QUnit is 7 years old and it's still in active development. It does not mean it's old. It's mature and opinionated. Without a lean API, it would probably be unmaintainable today.

---

## Past year releases

### QUnit 1.16.0 - Dec 3, 2014

- Core: Implements [QUnit.skip](http://api.qunitjs.com/QUnit.skip/)
- Async: Tests are now Promise-aware
- Async: Implement assert.async
- Test: Rename module's setup/teardown to beforeEach/afterEach

### QUnit 1.17.0 - Jan 19, 2015

- Build: Support Node.js export parity with CommonJS

### QUnit 1.17.1 - Jan 20, 2015

- Oops!

### QUnit 1.18.0 - Apr 3, 2015

- Assert: Implements notOk to assert falsy values
- Core: More graceful handling of AMD
- HTML Reporter: New diff using Google's Diff-Patch-Match Library

### QUnit 1.19.0 - Sep 1, 2015

- Assert: Add support to ES6' Map and Set equiv objects
- Core: Implement QUnit.stack

### QUnit 1.20.0 - Oct 27, 2015

- Assert: Add a calls count parameter on assert.async
- Core: Implement [QUnit.only](http://api.qunitjs.com/QUnit.only/)
- Core: Support Symbol types on QUnit.equiv
- Core: Implement [Nested modules](http://api.qunitjs.com/QUnit.module/)

#### Nested Modules

```js
QUnit.module( "grouped tests argument hooks", function( hooks ) {
  hooks.beforeEach( function( assert ) {
    assert.ok( true, "beforeEach called" );
  } );

  hooks.afterEach( function( assert ) {
    assert.ok( true, "afterEach called" );
  } );

  QUnit.test( "call hooks", function( assert ) {
    assert.expect( 2 );
  } );

  QUnit.module( "stacked hooks", function( hooks ) {

    // This will run after the parent module's beforeEach hook
    hooks.beforeEach( function( assert ) {
      assert.ok( true, "nested beforeEach called" );
    } );

    // This will run before the parent module's afterEach
    hooks.afterEach( function( assert ) {
      assert.ok( true, "nested afterEach called" );
    } );

    QUnit.test( "call hooks", function( assert ) {
      assert.expect( 4 );
    } );
  } );
} );
```

## Next releases before 2.0

Ref https://github.com/jquery/qunit/issues/891

- EventEmitter - PR at #882 - Based on [JS Reporters' specs](https://github.com/js-reporters/js-reporters)
- `QUnit.reporter` method with built-in tap - jquery/qunit#890
- Throw **warnings** for deprecated messages - jquery/qunit#881
- Release the last QUnit 1.x before QUnit 2 (no new features until QUnit 2)

## QUnit 2.0

- Remove the deprecated methods
- Apply the breaking changes with warnings (see https://github.com/jquery/qunit/milestones/v2.0)
- Release QUnit 2.0 / drops support for ES3 / change support to ES5+

## After QUnit 2.0

- Remove the warnings for methods removed in QUnit 2.0
- Release QUnit 2.1
- A lot of features to release - https://waffle.io/jquery/qunit

---

## Upgrading to QUnit 2.0

Running the last QUnit 1.x.x version without any deprecation warnings will probably result in a flawless and easy migration to QUnit 2.0.

## More and more features still coming

- [QUnit.pending](git@github.com:leobalter/qunit-roadmap.git)
- [Integration with chai.js](https://github.com/jquery/qunit/issues/864)
- [beforeAll/afterAll hooks](https://github.com/jquery/qunit/issues/893)
- ?

See more at https://waffle.io/jquery/qunit
