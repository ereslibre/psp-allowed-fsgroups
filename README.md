# Kubewarden policy psp-allowed-fsgroups

## Description

Replacement for the Kubernetes Pod Security Policy that controls the
usage of `fsGroup` in the pod security context.

## Settings

This policy works by defining what `fsGroup` is allowed in the pod security context.

One of the following setting keys are accepted for this policy:

* `MustRunAs`: contains a list of ranges that define valid ranges for the `fsGroup` value. At least
  one range must contain the provided `.securityContext.fsGroup`. If the pod does not contain a
  `.securityContext`, or a `.securityContext.fsGroup`, then this policy acts as mutating and
  defaults the `fsGroup` attribute to the first `min` value of the list of provided ranges.
* `MayRunAs`: contains a list of ranges that define valid ranges for the `fsGroup` value. At least
  one range must contain the provided `.securityContext.fsGroup`. If the pod does not contain a
  `.securityContext` or a `.securityContext.fsGroup`, then this policy will accept the request.
* `RunAsAny`: always accepts the request.

Configuration examples:

```yaml
rule: RunAsAny
```

```yaml
rule: MayRunAs
ranges:
  - min: 1000
    max: 2000
  - min: 3000
    max: 4000
```

```yaml
rule: MustRunAs
ranges:
  - min: 1000 # If no fsGroup is set for the pod, the
              # policy will default it to this value
    max: 2000
  - min: 3000
    max: 4000
```

## License

```
Copyright (C) 2021 Rafael Fernández López <rfernandezlopez@suse.com>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
