# Issue Description

The [documentation](https://docs.npmjs.com/cli/v11/commands/npx#:~:text=Whatever%20packages%20are,packages%20are%20available.) for `npx` describes an alternative way of specifying a package and it's version to help deal with situations where the name of a binary from some package may not match the package name. It's also possible to provide multiple packages to `npx` via repeated uses of this argument. This is useful for cases where a package may require multiple other packages to be specified at the same time to function properly.

`knip` successfully identifies the classic `npx` use case ignores it when reporting missing dependencies. But, for this newer use case it seems to falsely report missing dependencies.

## Repo Structure

To properly reproduce this issue, it suffices to have a `package.json` file with scripts that use `npx` and `knip`.

The `package.json` contains two entries in the script field `knip:with-arg` and `knip:without-arg`. Both run successfully, but in both cases, `knip` erroneously reports a missing dependency. If we delete the `knip:with-arg` entry or rework it to use the formulation outlined in `knip:without-arg` the issue goes away.

## Reproduction Steps

```shell
npm run knip:without-arg # or npm run knip:with-arg
```

Output seen locally:

```shell
someone@somewhere knip-npx-package-arg-issue % npm run knip:without-arg
> knip-npx-package-arg-issue@1.0.0 knip:without-arg
> npx knip@^5 --dependencies

Unlisted binaries (1)
knip  package.json
```