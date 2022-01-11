- Start Date: 2022/01/11 23:23:15
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

create **manipulate** workflow or generator to `copy/mv/manipulate` files.

# Basic example

```yaml
job: PNPM Workflow
  - action: replace
    paths: '*.js'
  - use: gulp-css
```

publish this yaml file as npm package or use directly

`neo run <npm-pkg|./gen.yaml>` to exec action in this file.

# Motivation

**prepack**

neo built in `prepack` command, it's a minimal generator, to prepack ci files, husky etc..., So neo has to built in workflow assets files and `husky` and so on...

these assets files should not builtin, builtin make `prepack` limit to pnpm project, not for yarn or npm project

So, we should create generator like above, make `prepack` much robust, let assets out of box

**create**

after created project from template, have to manual modify file content, like pkg name and remote url

# Detailed design

```yaml
job: PNPM Workflow
  - action: replace
    paths: '*.js'
  - use: gulp-css
```

will convert into gulp task list

- `action: replace` mean neo built in gulp-replace to replace content
- `use: gulp-css` mean it will load from external npm-pkg as gulp task

# Drawbacks

- gulp improve neo-pkg
- hard to test template generator

# Alternatives

- manual copy files from configs

# Adoption strategy

- neo should builtin **at least one official generator** as prepack default method

# Unresolved questions

- use majo or gulp
- `use` how to load remote pkg