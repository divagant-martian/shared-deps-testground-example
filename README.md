


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