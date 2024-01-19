---
title: JS Export Files
date-modified: 2024-01-19
---

I have a personal grudge against files like this:

```
export * from './input'
export * from './input-field'
export * from './check-label'
export * from './checkbox'
export * from './dropdown'
export * from './icons'
export * from './loader'
// ... And so on
```

There are few reasons why this is suboptimal, one of which is name clashing.

For example `./input` file should be allowed to, say `export type Props` (instead of the verbose `export type InputProps`).

but then `index.ts` cannot do:
```
export * from './input';
export * from './button';
```

because both `input` and `button` might export `Props` type.
so we have to choose. We can do:

`button.tsx`:
```
export type ButtonProps = { ... }
// instead of more preferable
// export type Props = { ... }
```

or we need to juggle `index.ts` files to do:
```
export { Input } from './input';
export type { Props as InputProps } from './input';
```

but this is not very ergonomic. Ultimate solution is to have
per-component exports:

```
import { Input, Props } from '@dhub/ui/input'
// in case of name clash we can rename at use-site:
import { Button, Props as ButonProps } from '@dhub/ui/button'
```

this way `index.ts` export file is not needed at all.

to achieve `@dhub/ui/input` path, we can leverage `package.json` `exports` field:
```
{
  "exports": {
    ".": "./dist/index.js",
    "./input": "./dist/input.js"
  }
}
```

this can be automated

