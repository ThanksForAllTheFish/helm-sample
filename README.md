# What I don't understand

Go in `standard-service` and run `helm dependency update`, then `helm install --dry-run --debug .`. You get (as I expect):

```
COMPUTED VALUES:
standard-service:
  domain: example.com
```

Go in `helm-sample`, run `helm dependency update`, then `helm install --dry-run --debug .`. You get:

```
COMPUTED VALUES:
resources: {}
standard-service:
  global: {}
  standard-service:
    env: example
```

- Why `standard-service.standard-service`? I guess it is due to the double indirection layer, though I think it would be more intuitive to flatten.
- Why no reference to `standard-service42` (`helm-sample/requirements.yaml` kinda indicates that is an alias for `base-service`, somehow I would expect to pick the default values to be picked up as per `standard-service`).
-- Run `helm install --dry-run --debug --set standard-service42.enabled=true .`, now default values are loaded.
