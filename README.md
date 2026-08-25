# matrix-ops-core

Dense linear algebra for JavaScript and TypeScript. Create matrices, run element-wise and matrix products, factorize, invert, and solve linear systems — all in one package.

Works in Node.js and the browser (ESM, CommonJS, and UMD).

```bash
npm install matrix-ops-core
```

```js
import { Matrix, SVD, inverse, solve } from 'matrix-ops-core';

const X = new Matrix([
  [4, 1, 2],
  [1, 5, 0],
  [2, 0, 3],
]);

X.mmul(inverse(X)); // ≈ I
```

Repository: [github.com/Ops-Core/matrix](https://github.com/Ops-Core/matrix)

---

## What you get

| Area | Highlights |
| --- | --- |
| Construction | `new Matrix(...)`, `zeros`, `ones`, `eye`, `diag`, `rand`, row/column vectors |
| Arithmetic | `add` / `sub` / `mul` / `div` / `mod`, `mmul`, `mpow`, Kronecker product |
| Shape | transpose, concat, views, wrap existing typed arrays without copying |
| Stats | mean, variance, norm, covariance, correlation, `applyAlongAxis` |
| Factorization | LU, QR, SVD, EVD, Cholesky, NIPALS |
| Solvers | `solve`, `inverse`, `pseudoInverse`, `determinant` |
| Special types | `SymmetricMatrix`, `DistanceMatrix` |

Type definitions ship with the package (`matrix.d.ts`).

---

## Quick start

ESM:

```js
import { Matrix } from 'matrix-ops-core';

const A = Matrix.eye(3);
const b = Matrix.columnVector([1, 2, 3]);
```

CommonJS:

```js
const { Matrix } = require('matrix-ops-core');
```

Browser (UMD, via unpkg / jsDelivr): `matrix.umd.js`.

---

## Building matrices

```js
import { Matrix } from 'matrix-ops-core';

const fromRows = new Matrix([
  [2, 0, -1],
  [0, 3, 4],
]);

const empty = Matrix.zeros(4, 4);
const identity = Matrix.eye(4);
const diagonal = Matrix.diag([3, 5, 7]);
const noise = Matrix.rand(8, 8, { random: Math.random });

fromRows.rows;    // 2
fromRows.columns; // 3
fromRows.get(1, 2); // 4
fromRows.set(0, 1, 9);
```

`wrap()` puts a matrix interface over an existing 1D or 2D array so you can reuse buffers:

```js
import { wrap } from 'matrix-ops-core';

const buffer = Float64Array.from([1, 2, 3, 4, 5, 6]);
const view = wrap(buffer, { rows: 2 });
view.set(0, 0, 10); // writes through to `buffer`
```

---

## Arithmetic

Static methods return a new matrix. Instance methods mutate in place.

```js
import { Matrix } from 'matrix-ops-core';

const P = new Matrix([
  [1, 2],
  [3, 4],
]);
const Q = new Matrix([
  [0, 5],
  [6, 7],
]);

Matrix.add(P, Q);  // new matrix
P.add(Q);          // P is updated

P.mmul(Q);         // matrix product
P.mul(0.5);        // scale
P.mpow(3);         // P³ via exponentiation by squaring
```

Element-wise math follows `Math.*` names: `abs`, `exp`, `log`, `sqrt`, `sin`, `cos`, and the rest of the standard set. Call them statically (`Matrix.exp(P)`) or in place (`P.exp()`).

Reductions and geometry:

```js
P.mean();
P.norm();          // Frobenius
P.transpose();
P.diag();
P.concat(Q, 'column');
P.applyAlongAxis((col) => col.reduce((s, v) => s + v, 0), 'column');
```

---

## Linear systems

```js
import { Matrix, inverse, solve, pseudoInverse, determinant } from 'matrix-ops-core';

const A = new Matrix([
  [3, 1, 0],
  [1, 4, 1],
  [0, 1, 2],
]);
const b = Matrix.columnVector([5, 6, 3]);

const x = solve(A, b);
const Ainv = inverse(A);
determinant(A);

// Rank-deficient / rectangular: SVD-based inverse
const tall = new Matrix([
  [1, 0],
  [1, 1],
  [0, 1],
]);
inverse(tall, true);
tall.pseudoInverse();
```

`solve` uses LU when the left-hand side is square and QR otherwise. Pass `true` as the third argument to force SVD (useful when the system is singular).

---

## Factorizations

```js
import {
  Matrix,
  LU,
  QR,
  SVD,
  EVD,
  CHO,
  NIPALS,
} from 'matrix-ops-core';

const M = new Matrix([
  [6, 2, 1],
  [2, 5, 2],
  [1, 2, 4],
]);

const { lowerTriangularMatrix: L, upperTriangularMatrix: U } = new LU(M);
const { orthogonalMatrix: Q, upperTriangularMatrix: R } = new QR(M);

const svd = new SVD(M);
svd.diagonal;      // singular values
svd.leftSingularVectors;
svd.rightSingularVectors;

const evd = new EVD(M);
evd.realEigenvalues;
evd.eigenvectorMatrix;

new CHO(M).lowerTriangularMatrix;

const nipals = new NIPALS(M);
nipals.t; // scores
nipals.p; // loadings
```

Full class names (`LuDecomposition`, `QrDecomposition`, `SingularValueDecomposition`, …) are exported alongside the short aliases.

---

## Symmetric and distance matrices

```js
import { SymmetricMatrix, DistanceMatrix } from 'matrix-ops-core';

const S = SymmetricMatrix.ones(4);
S.set(0, 3, 2); // also sets (3, 0)

const D = DistanceMatrix.fromCompact([1.2, 0.8, 3.1]);
```

---

## Stats helpers

```js
import { Matrix, covariance, correlation } from 'matrix-ops-core';

const samples = new Matrix([
  [1.0, 2.1, 0.4],
  [1.2, 1.9, 0.5],
  [0.8, 2.4, 0.3],
  [1.1, 2.0, 0.6],
]);

covariance(samples);
correlation(samples);
```

---

## Scripts

```bash
npm test          # unit tests, eslint, prettier
npm run compile   # rollup bundles
```

---

## License

[MIT](./LICENSE) — jamesmorse82
