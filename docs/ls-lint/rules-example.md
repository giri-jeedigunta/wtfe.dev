# Examples rules with ls-lint

Read - https://wtfe.dev/posts/fe/ls-lint/

## Desired Folder and File structure example: 

```sh
📦src
 ┣ 📂hooks
 ┃ ┗ 📂useFooBar
 ┃ ┃ ┣ 📜index.ts
 ┃ ┃ ┣ 📜useFooBar.test.ts
 ┃ ┃ ┗ 📜useFooBar.ts
 ┣ 📂utils
 ┃ ┗ 📂getFooBar
 ┃ ┃ ┣ 📂getFooBar.test.ts
 ┃ ┃ ┣ 📂getFooBar.ts
 ┃ ┃ ┗ 📜index.ts
 ┃ 📂components
 ┃ ┃ ┗ 📂FooBar
 ┃ ┃ ┃ ┣ 📂FooBar.module.scss
 ┃ ┃ ┃ ┣ 📂FooBar.srories.tsx
 ┃ ┃ ┃ ┣ 📂FooBar.test.tsx
 ┃ ┃ ┃ ┣ 📂FooBar.tsx
 ┃ ┃ ┃ ┗ 📜index.ts
```

 ## ls-lint rules that can enforce them

 Create a `.ls-lint.yaml` in the root and copy these rules. 
 
 To test run `npx ls-lint`. Play around by introducing different folder structures and rules. 

 ```yaml
ls:
  # Enforce that only "hooks", "utils", and "components" exist in `src/`
  src/*/:
    .dir: regex:^(hooks|utils|components)$

  src/hooks/*/:
    # Hooks must be prefixed with "use" and be in PascalCase
    .dir: regex:^use[A-Z][a-zA-Z0-9]+$
    .ts: camelCase

  src/utils/*/:
    # Utility function folders should be camelCase
    .dir: camelCase
    .ts: camelCase

  src/components/*/:
    # Components must be PascalCase, including related files
    .dir: PascalCase
    .module.scss: PascalCase
    .stories.tsx: PascalCase
    .tsx: PascalCase
    .test.tsx: PascalCase
    .ts: camelCase

  # Enforcing depth: components cannot have nested "components" folder
  src/components/*/components:
    .dir: exists:0

 ```