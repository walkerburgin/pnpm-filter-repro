# pnpm-filter-repro

## Overview
We have a large monorepo that uses PNPM. Our build system calls `pnpm install` using the `--filter` argument to install dependencies
for the subset of the repository that a developer is working on. The ability to perform a filtered install like this was actually the
killer feature that led us adopt PNPM in the first place. It looks like the `--filter` argument may have been broken in the
`v8.0.0` release.


## Repro

This repository has two disjoint sets of packages:
* `@monorepo/foo-app` -> `@monorepo/foo-lib`
* `@monorepo/bar-app` -> `@monorepo/bar-lib`

My expectation is that running `pnpm install --filter @monorepo/foo-app...` will not install dependencies for `@monorepo/bar-app`
or `@monorepo/bar-lib`.


### `v7.33.6`

```bash
➜ pnpm-filter-repro node pnpm/v7.33.6/bin/pnpm.cjs install --filter @monorepo/foo-app...
```

```bash
➜ pnpm-filter-repro tree -d packages
packages
├── bar-app
├── bar-lib
├── foo-app
│   └── node_modules
│       ├── @monorepo
│       │   └── foo-lib -> ../../../foo-lib
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       ├── react-dom -> ../../../node_modules/.pnpm/react-dom@18.2.0_react@18.2.0/node_modules/react-dom
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
└── foo-lib
    └── node_modules
        ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
        └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
```

### `v8.0.0`

```bash
➜ pnpm-filter-repro node pnpm/v8.0.0/bin/pnpm.cjs install --filter @monorepo/foo-app...
```

```bash
➜ pnpm-filter-repro tree -d packages
packages
├── bar-app
│   └── node_modules
│       ├── @monorepo
│       │   └── bar-lib -> ../../../bar-lib
│       ├── cypress -> ../../../node_modules/.pnpm/cypress@13.0.0/node_modules/cypress
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       ├── react-dom -> ../../../node_modules/.pnpm/react-dom@18.2.0_react@18.2.0/node_modules/react-dom
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
├── bar-lib
│   └── node_modules
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
├── foo-app
│   └── node_modules
│       ├── @monorepo
│       │   └── foo-lib -> ../../../foo-lib
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       ├── react-dom -> ../../../node_modules/.pnpm/react-dom@18.2.0_react@18.2.0/node_modules/react-dom
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
└── foo-lib
    └── node_modules
        ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
        └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
```

### `v8.9.2`

```bash
➜ pnpm-filter-repro node pnpm/v8.9.2/bin/pnpm.cjs install --filter @monorepo/foo-app...
```

```bash
➜ pnpm-filter-repro tree -d packages
packages
├── bar-app
│   └── node_modules
│       ├── @monorepo
│       │   └── bar-lib -> ../../../bar-lib
│       ├── cypress -> ../../../node_modules/.pnpm/cypress@13.3.3/node_modules/cypress
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       ├── react-dom -> ../../../node_modules/.pnpm/react-dom@18.2.0_react@18.2.0/node_modules/react-dom
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
├── bar-lib
│   └── node_modules
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
├── foo-app
│   └── node_modules
│       ├── @monorepo
│       │   └── foo-lib -> ../../../foo-lib
│       ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
│       ├── react-dom -> ../../../node_modules/.pnpm/react-dom@18.2.0_react@18.2.0/node_modules/react-dom
│       └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
└── foo-lib
    └── node_modules
        ├── react -> ../../../node_modules/.pnpm/react@18.2.0/node_modules/react
        └── typescript -> ../../../node_modules/.pnpm/typescript@5.2.2/node_modules/typescript
```
