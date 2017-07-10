# Writing a commit

Our approach to commits follows Stephen Ball's [_Deliberate Git_](http://www.rakeroutes.com/blog/deliberate-git/) philsoophy. You can [watch a video of his presentation](https://vimeo.com/72762735) of this philosophy from Steel City Ruby 2013.

> “Your code can only say what it does right now. You can’t look at a method and see its history: the alternative approaches that have been considered, the algorithms that have already been outgrown, the simpler code that has been replaced, or the complicated code that’s been refactored.Not capturing this knowledge is a huge loss. In Deliberate Git I'll share how to use Git to write detailed commits that craft a cohesive story about the code without giving up a good programming flow.”
>
> Stephen Ball @ Steel City Ruby 2013

## Commit criteria

Good commits answer the following questions, as applicable.

- Does the commit title state what this commit will do when merged?
- Does the commit body explain why the change was required?
- Is it clear why this approach was taken over others?
- Was there research conducted that would be beneficial for another developer to know?
- If you used a 3rd-party site like StackOverflow or a developer’s blog post, is that resource referenced in the commit message?
- Are there conditions in which this approach might no longer be appropriate?
- Would another developer understand full scope of the change and how to leverage or extend it?

## Examples

A list of excellent commits within CoA projects has been compiled in [commits.md](commits.md).