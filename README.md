<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# cumax

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Compute the cumulative maximum value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

<section class="installation">

## Installation

```bash
npm install @stdlib/stats-cumax
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var cumax = require( '@stdlib/stats-cumax' );
```

#### cumax( x\[, options] )

Computes the cumulative maximum value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = cumax( x );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ -1.0, 2.0, 2.0 ]
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].
-   **dtype**: output ndarray [data type][@stdlib/ndarray/dtypes]. Must be a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].

By default, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor]. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});

var v = ndarray2array( x );
// returns [ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

var y = cumax( x, {
    'dims': [ 0 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 2.0 ], [ -1.0, 4.0 ] ]

y = cumax( x, {
    'dims': [ 1 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

y = cumax( x, {
    'dims': [ 0, 1 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 2.0 ], [ 2.0, 4.0 ] ]
```

By default, the function returns an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] determined by the function's output data type [policy][@stdlib/ndarray/output-dtype-policies]. To override the default behavior, set the `dtype` option.

```javascript
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var getDType = require( '@stdlib/ndarray-dtype' );
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0 ], {
    'dtype': 'generic'
});

var y = cumax( x, {
    'dtype': 'float64'
});
// returns <ndarray>

var dt = getDType( y );
// returns 'float64'
```

#### cumax.assign( x, out\[, options] )

Computes the cumulative maximum value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [ndarray][@stdlib/ndarray/ctor].

```javascript
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var array = require( '@stdlib/ndarray-array' );
var zerosLike = require( '@stdlib/ndarray-zeros-like' );

var x = array( [ -1.0, 2.0, -3.0 ] );
var y = zerosLike( x );

var out = cumax.assign( x, y );
// returns <ndarray>

var v = ndarray2array( out );
// returns [ -1.0, 2.0, 2.0 ]

var bool = ( out === y );
// returns true
```

The method has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a real-valued or generic [data type][@stdlib/ndarray/dtypes].
-   **out**: output [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The method accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Both functions iterate over [ndarray][@stdlib/ndarray/ctor] elements according to the memory layout of the input [ndarray][@stdlib/ndarray/ctor].
-   The output data type [policy][@stdlib/ndarray/output-dtype-policies] only applies to the main function and specifies that, by default, the function must return an [ndarray][@stdlib/ndarray/ctor] having the same [data type][@stdlib/ndarray/dtypes] as the input [ndarray][@stdlib/ndarray/ctor]. For the `assign` method, the output [ndarray][@stdlib/ndarray/ctor] is allowed to have any supported output [data type][@stdlib/ndarray/dtypes].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-array-discrete-uniform' );
var getDType = require( '@stdlib/ndarray-dtype' );
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var ndarray = require( '@stdlib/ndarray-ctor' );
var cumax = require( '@stdlib/stats-cumax' );

// Generate an array of random numbers:
var xbuf = discreteUniform( 25, 0, 20, {
    'dtype': 'generic'
});

// Wrap in an ndarray:
var x = new ndarray( 'generic', xbuf, [ 5, 5 ], [ 5, 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

// Perform operation:
var y = cumax( x, {
    'dims': [ 0 ]
});

// Resolve the output array data type:
var dt = getDType( y );
console.log( dt );

// Print the results:
console.log( ndarray2array( y ) );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/stats-cumax.svg
[npm-url]: https://npmjs.org/package/@stdlib/stats-cumax

[test-image]: https://github.com/stdlib-js/stats-cumax/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/stats-cumax/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/stats-cumax/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/stats-cumax?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/stats-cumax.svg
[dependencies-url]: https://david-dm.org/stdlib-js/stats-cumax/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/stats-cumax/tree/deno
[deno-readme]: https://github.com/stdlib-js/stats-cumax/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/stats-cumax/tree/umd
[umd-readme]: https://github.com/stdlib-js/stats-cumax/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/stats-cumax/tree/esm
[esm-readme]: https://github.com/stdlib-js/stats-cumax/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/stats-cumax/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/stats-cumax/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes

[@stdlib/ndarray/output-dtype-policies]: https://github.com/stdlib-js/ndarray-output-dtype-policies

</section>

<!-- /.links -->
