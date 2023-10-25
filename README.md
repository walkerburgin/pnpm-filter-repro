# pnpm-filter-repro

## `v7.33.6`

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

## `v8.9.2`

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
