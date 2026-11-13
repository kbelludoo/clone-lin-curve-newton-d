# clone-lin-curve-newton-d

Experimental **LIN** clone of Curve Finance tricrypto
`CurveCryptoMathOptimized3.newton_D` (Newton solver for invariant `D` given
three scaled balances).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [curvefi/tricrypto-ng](https://github.com/curvefi/tricrypto-ng) `ecaa8161c240f21dd7c3712eefc5637e1dac742b`
  - `contracts/main/CurveCryptoMathOptimized3.vy` sha256 `d0d48e5c3fa00e36f841250cbce8665292ba3224bb050c948dc3b12a50f01d6c` blob `695c794cb8035e4b2848ad0354d0993dcfb9c7cb`
  - Curve.Fi publishes that tree as informational-only (no reproduction license). This repository does **not** vendor the Vyper source.
- **LIN kernel:** [`src/lin_curve_newton_d.lin`](src/lin_curve_newton_d.lin) (sha256 `6dbfd10b2d8d11689d142b0ae5cd838d98b8046f0db5fe95cfaf967ccdfe3949`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/curve_newton_d_c11.c`](test/oracles/curve_newton_d_c11.c)
- **Proofs (lin-open only):** `examples/curve_newton_d/` and `make curve-newton-d-proof`
- **Class:** EXPERIMENTAL uint64-scale, `SCALE = 1e9`. Not Ethereum tricrypto uint256. Not `price_scale` / `_newton_y` / `K0_prev` cbrt apriori. Not a production pool replacement.

Named goldens (equal `1e9` balances, `ANN=1707629`, `gamma=11809`): identity **D=3000000000**; `x0 += 10%` → **D=3096846429** `vp=998982719`; imbalanced `(1.2e9,0.9e9,1e9)` **D=3077962761**; `K0_prev!=0` fail-closed **0**; `ANN=MIN_A=2700` fail-closed **0** (`mul1` exceeds signed i64). Naive i64 `3e9 * 508044030482641` wraps to **6755845818716831232**.

## Reproduce proofs (in lin-open)

```bash
make curve-newton-d-proof
# or: python3 test/prove_curve_newton_d_external.py
```

## Not claimed

Uint256 / ONE=1e18 / price_scale mainnet parity. `K0_prev` cubic-root apriori.
LIN replacing Curve or the EVM. TVL or dollar savings. zk soundness.
Stableswap `get_D` / `_newton_y` (see clone-lin-curve-vp / clone-lin-curve-newton-y).
