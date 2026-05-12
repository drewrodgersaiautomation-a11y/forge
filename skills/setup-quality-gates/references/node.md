# Quality Gates: Node / TypeScript

## Detect package manager

Check for lockfiles: `package-lock.json` (npm), `pnpm-lock.yaml` (pnpm), `yarn.lock` (yarn), `bun.lockb` (bun). Default to npm if unclear.

## Install dependencies

```bash
npm install -D husky lint-staged prettier eslint
```

For TypeScript projects also install:
```bash
npm install -D typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

## Initialize Husky

```bash
npx husky init
```

## Create `.husky/pre-commit`

```
npx lint-staged
npm run typecheck || true
npm run test
```

Omit `typecheck` or `test` lines if those scripts don't exist in `package.json`. Tell the user which were omitted.

## Create `.lintstagedrc`

```json
{
  "*.{js,jsx,ts,tsx}": ["eslint --fix", "prettier --write"],
  "*.{json,md,css,html}": ["prettier --write"]
}
```

## Create `.prettierrc` (if missing)

```json
{
  "useTabs": false,
  "tabWidth": 2,
  "printWidth": 80,
  "singleQuote": false,
  "trailingComma": "es5",
  "semi": true,
  "arrowParens": "always"
}
```

## Create `.eslintrc.json` (if missing)

For TypeScript:
```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  "rules": {
    "no-unused-vars": "off",
    "@typescript-eslint/no-unused-vars": ["error"],
    "@typescript-eslint/no-explicit-any": ["warn"]
  }
}
```

## Add scripts to package.json

Ensure these exist:
```json
{
  "scripts": {
    "prepare": "husky",
    "typecheck": "tsc --noEmit",
    "lint": "eslint ."
  }
}
```
