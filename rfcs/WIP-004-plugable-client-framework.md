- Start Date: 2022/08/07
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

a react ui framework, page plugable. dynamic create page with single npm package.

# Basic example

TODO

# Motivation

mario workflow ui need a client page to display or edit workflow on page. It should be standalone, not relay on neo
core page.

however, neo also use `mario`, also need `mario` page and also display others page not releated to mario. 

If mario provide a standalone npm package, `pluginable-framework` dynamic
load npm package to create page. 

Inside mario, mario also re-use this npm package to create page based on `pluginable-framework`.

- neo load mario package ui client, and display others pages from other npm packages or built-in pages
- mario load mario package ui client

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

# Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on users
- integration of this feature with other existing and planned features
- cost of migrating (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy

If we implement this proposal, how will existing users adopt it? Is
this a breaking change? Can we write a codemod? Can we provide a runtime adapter library for the original API it replaces? 

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?