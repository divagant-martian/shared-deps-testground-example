


```sh
testground plan import --from ./ --name "shared-deps-testground-example"
```

```sh
testground run composition -f ./composition_a.toml --wait
```

```sh
PLAN_NAME=plan_a PLAN_CASE=plan_a testground run composition -f ./composition_generic.toml --wait

PLAN_NAME=plan_b PLAN_CASE=plan_b testground run composition -f ./composition_generic.toml --wait
```

First run
```
Step 9/14 : RUN cargo chef cook --release --recipe-path recipe.json
 ---> Running in e3e54496987e
    Updating crates.io index
   Compiling serde v1.0.147
   Compiling serde_json v1.0.87
   Compiling itoa v1.0.4
   Compiling ryu v1.0.11
   Compiling utility v0.0.1 (/test-plan/utility)
   Compiling plan_a v0.0.1 (/test-plan/plan_a)
   Compiling plan_b v0.0.1 (/test-plan/plan_b)
    Finished release [optimized] target(s) in 9.46s
 ---> 760a124b8aa0
Step 10/14 : COPY ./plan .
 ---> f2027d9f4e2e
Step 11/14 : RUN cargo build --release -p plan_a
 ---> Running in 0e45c8f284ca
   Compiling utility v0.1.0 (/test-plan/utility)
   Compiling plan_a v0.1.0 (/test-plan/plan_a)
```
 
Second run
```
Step 9/14 : RUN cargo chef cook --release --recipe-path recipe.json
 ---> Using cache
 ---> 760a124b8aa0
Step 10/14 : COPY ./plan .
 ---> d81aa629f90d
Step 11/14 : RUN cargo build --release -p plan_a
 ---> Running in 3c2ae55d98fa
   Compiling utility v0.1.0 (/test-plan/utility)
   Compiling plan_a v0.1.0 (/test-plan/plan_a)
```
