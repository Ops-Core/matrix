# Changelog

Release notes for [matrix-ops-core](https://github.com/Ops-Core/matrix). Each heading matches a git tag.

## [1.0.0](https://github.com/Ops-Core/matrix/releases/tag/1.0.0) — 2026-08-25

Stable public API.

- Freeze construction, arithmetic, solvers, and factorization exports
- Document ESM, CommonJS, and UMD entry points
- Ship TypeScript definitions with the package

## [0.9.0](https://github.com/Ops-Core/matrix/releases/tag/0.9.0) — 2026-07-18

- Add `concat` along a chosen axis
- Add `applyAlongAxis` for row/column reductions
- Add `mpow` (exponentiation by squaring)
- Add `gram` and `mmulByTranspose`

## [0.8.0](https://github.com/Ops-Core/matrix/releases/tag/0.8.0) — 2026-06-12

- Add `SymmetricMatrix` and `DistanceMatrix`
- Support compact 1D import (`fromCompact`)
- Add NIPALS factorization

## [0.7.0](https://github.com/Ops-Core/matrix/releases/tag/0.7.0) — 2026-05-09

- Add covariance and correlation helpers
- Add mean, variance, product, and Frobenius `norm`
- Add min/max by row or column

## [0.6.0](https://github.com/Ops-Core/matrix/releases/tag/0.6.0) — 2026-04-03

- Add matrix views (row, column, submatrix, transpose, selection)
- Add `wrap` for 1D and 2D buffers without copying
- Add `WrapperMatrix1D` and `WrapperMatrix2D`

## [0.5.0](https://github.com/Ops-Core/matrix/releases/tag/0.5.0) — 2026-03-07

- Add eigenvalue decomposition (EVD)
- Add Cholesky decomposition
- Add `linearDependencies`

## [0.4.0](https://github.com/Ops-Core/matrix/releases/tag/0.4.0) — 2026-02-14

- Add SVD
- Add `inverse`, `pseudoInverse`, and `solve`
- Add SVD-backed paths for singular and rectangular systems
- Add `determinant`

## [0.3.0](https://github.com/Ops-Core/matrix/releases/tag/0.3.0) — 2026-01-22

- Add LU and QR decompositions
- Add Kronecker product
- Add `transpose` and diagonal helpers

## [0.2.0](https://github.com/Ops-Core/matrix/releases/tag/0.2.0) — 2025-12-11

- Add element-wise `add`, `sub`, `mul`, `div`, `mod` (static and in-place)
- Add matrix product `mmul`
- Add `Math.*` element-wise maps (`abs`, `exp`, `log`, `sqrt`, `sin`, `cos`, …)

## [0.1.0](https://github.com/Ops-Core/matrix/releases/tag/0.1.0) — 2025-11-04

Initial release.

- Construct matrices from nested arrays
- Factories: `zeros`, `ones`, `eye`, `diag`, `rand`, row and column vectors
- `get` / `set`, size, and basic shape checks
