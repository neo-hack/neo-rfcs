- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Target Major Version: (2.x / 3.x)
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

Brief explanation of the feature.

# Basic example

If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.

# Motivation

我现在使用 `ts & rust`, 未来还会使用 `go`. 现在 `prepack` 

问题：

- Q1 `prepack` 定位问题
- Q2 `prepack` 无法设置其他项目的工作流

如果只是预想中的那样，控制 `workflows`，那么另外的文件怎么办，比如说`.eslintrc, .gitignore`。另外，`prepack` 还会修改文件。这部分工作和 `generator(WIP, No RFC)`重合了。

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

**Plan B & C** 应该一起实现，`C`在`B`之后。

# Detailed design

github workflows

## How to use it

maybe `neo prepack(better) --module=ci` or `neo ci` to select what kinds of ci workflows

## How to design workflow

put into workflows into `preset`

```json
{
  "workflows": [
    {
      "name": "ci", // workflow id
      "workflow: "workflow" // workflow filepath
    }
  ]
}
```

# Drawbacks
> TODO

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people Vue
- integration of this feature with other existing and planned features
- cost of migrating existing Vue applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives
> TODO

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy
> TODO

If we implement this proposal, how will existing Vue developers adopt it? Is
this a breaking change? Can we write a codemod? Can we provide a runtime adapter library for the original API it replaces? How will this affect other projects in the Vue ecosystem?

# Unresolved questions
> TODO

Optional, but suggested for first drafts. What parts of the design are still
TBD?