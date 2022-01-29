- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

like github workflow define [outputs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-defining-outputs-for-a-job) of each job, steps, or global workflow variable

# Basic example

define [global outputs variable](https://docs.github.com/en/actions/using-workflows/reusing-workflows#using-inputs-and-secrets-in-a-reusable-workflow)

```yaml
on:
  workflow_call:
    inputs:
      username:
        required: true
        type: string
    secrets:
      envPAT:
        required: true
```

use `inputs.username`

in job and step

```yaml
jobs:
  steps:
    - uses: action
      with:
        input: ${{ inputs.username }}
```


# Motivation

after create project from `bin-template`, replace all `bin-template` to real project name.

# Detailed design

1. define global inputs on `workflow_call`

under same job

1. actions setup inputs 
   
   ```ts
   action() {
     ctx.setOutputs('key', value)
   }
   ```

2. use actions outputs by `steps.id.outputs.key`

# Drawbacks

- github outputs system is complex, share outputs between jobs need

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    # Map a step output to a job output
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "::set-output name=test::hello"
      - id: step2
        run: echo "::set-output name=test::world"
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
```

key is `needs: job1`, if implement same logic like that, may be make mario very complex

# Unresolved questions

- [ ] template syntax `<%= user %>` or `${{ inputs }}`