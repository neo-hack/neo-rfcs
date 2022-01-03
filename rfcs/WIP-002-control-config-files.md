- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Target Major Version: (2.x / 3.x)
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary
> new command maybe rc, or another name

read config of preset, select and copy from command line `neo rc` or `neo list --rc`.

# Basic example

`neo rc`

- `ci.yaml`
- `release yaml`

select and copy to clipboard

# Motivation

我现在使用 `ts & rust`, 未来还会使用 `go`. 现在 `prepack` 

问题：

- Q1 `prepack` 定位问题
- Q2 `prepack` 无法设置其他项目的工作流

如果只是预想中的那样，控制 `workflows`，那么另外的文件怎么办，比如说`.eslintrc, .gitignore`。另外，`prepack` 还会修改文件。这部分工作和 `generator(WIP, No RFC)`重合了。

# Detailed design

几种方案：

**Plan A**

只控制 `workflows`。命令执行过程

1. command
2. select workflows
3. auto create selected workflow in `github/workflows`

**Plan B**

任何 `config files`。命令执行过程

1. command
2. select config, copy to clipboard
3. manual create file, and whereever you want to put in.

**Plan C**

A & B 都不能已有文件。激进一点，是另外一种形式的 `generator`。前置条件是需要创建一个 `config generator`，前前置条件是需要完整的 `generator` 流程。(`generator` 设计目标是用来修改创建之后的项目，比如说重新命名项目文件。所以也可以满足这种使用条件）执行过程：

already has generator and config generator

1. command 
2. list already generator(type=config or workflow)
3. select generator and exec it(maybe exec parts of generator workflow will be exec)

**Plan B & C** 应该一起实现，`C`在`B`之后。这个RFC只会讨论`neo rc`。

**below config files supported**

- github workflows
- editor config
- eslint config
- issue template

## How to design workflow

put into configs into `preset`

```json
{
  "configs": [
    {
      "name": "ci", // workflow id
      "workflow: "workflow" // workflow filepath
    }
  ]
}
```

## How to use it

maybe `neo rc` or `neo list --ci` will read configs, and list, user will select what kinds of config file to copy.

# Drawbacks

- Not sure it's strong needed feature? [#alternatives](#alternatives) already list another option to implement it.
- View config detail maybe increase size, and not able to cover all file type syntax-highlight

# Adoption strategy

- preset-package will has new field named `config`, contain all configs

# Alternatives

1. copy paste manual from your other projects - `neo rc` is much fast
2. builtin generator, not to copy it, just run generator to mv & copy & modify these files to target place - `generator` is heavy, sometimes I know what config I want, I just want to copy it

# Unresolved questions

- command name, new command or just old command options