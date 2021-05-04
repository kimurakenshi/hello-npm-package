# hello-npm-package

A hello world example of how to publish [npm](https://www.npmjs.com/) packages to the [npm registry](https://www.npmjs.com/) using
a monorepo with [pnpm](https://pnpm.io/) as the package manager and [@changesets/cli](https://github.com/atlassian/changesets/tree/main/packages/cli)  to manage the versioning 
and changelog entries for your packages.

## Requirements

Install [pnpm](https://pnpm.io/installation).

## Project Setup

Before explaining the project structure we are going to review how this project was initialized:

1. Run `pnpm add -DW @changesets/cli` and then  `pnpx changeset init` to setup `changesets`
1. Check `baseBranch` in `.changeset/config.json` to make sure  is matching your main branch name.
1. Update the main package.json scripts section with ` "preinstall": "npx only-allow pnpm"` to force the usage of `pnpm`.
1. Create a new folder called `packages` where all your npm package are going to exist.
1. Create a `pnpm-workspace.yaml` file in the root path and update it to:

```yaml
   packages:
    - 'packages/*'
```

> This will be referencing workspace packages through their relative path.

1. Create `packages/hello-world` as the main folder that contains `hello-world` package. 
This package is scoped to my npm username as you can see in `packages/hello-world/package.json`:

```json
{
   "name": "@kimurakenshi/hello-npm-package"
}   
```

> Replace `@kimurakenshi` with your npm username or organization to test this out.
 
## How to release changes

There is a script in the main `package.json` that is basically that takes care of one particular step of the release process.

1. Once you have make changes that you want to include in a changeset just run `pnpm changeset`.
1. Run `pnpm bump` to bump the versions of the packages previously specified with `changeset`.
1. Run `pnpm install` to update the lockfile and rebuild packages.
1. Commit the changes.
1. Run `pnpm release` to publish all packages that have bumped versions not yet present in the registry.




