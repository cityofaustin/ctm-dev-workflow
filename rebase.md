# Using rebase to ensure a clean commit history

Git's [_rebase_](https://git-scm.com/docs/git-rebase) feature is a powerful and advanced tool that can help you convert a messy commit history into useful notes for future developers. Sometimes that future developer might even be you!

More precisely, the _interactive_ rebase feature can be used to re-write history to make it appear like you never made a mistake and wrote all of your perfect code in one try. Yes, it is sorcery. No, you do not need a Hogwarts degree perform it.

## Starting at a messy commit history

So you've done your work in your feature branch and, hopefully, have been generating frequent, isolated commits for your work in progress. When you run `$ git log` your history may look something like this:

```
commit 28f0fed0fbefab20436e9d0927d0e07241b1db05
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jun 28 13:25:05 2017 -0500

    wip workflow

commit 88c7675ef37489056ff0550cd3216d6c7599a99f
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jun 28 13:24:51 2017 -0500

    wip setup

commit cdf3bf1fde1c3c138eb73a020c375b70c7a22b65
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jun 28 13:00:27 2017 -0500

    wip local setup

commit 70adbee56a3b0a8e766e0eba120dc390813895ee
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jun 28 13:00:03 2017 -0500

    wip unified guides

commit 69bcb81dd6e1749560a51775e66a7befd6c6fd5e
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jun 28 08:35:43 2017 -0500

    wip aggregate all guides outside of workflow
```

## Initiating the interactive rebase

So you have a bunch of "wip" (work-in-progress) commits that you are now ready to do 2 things with:

1. Combine them into logical clusters of commits. In this example, all the commits that changed `workflow.md` should be grouped into one single commit that tells the story of one cohesive re-write of the file.
2. Provide thoughtful commit titles and messages to help future developers who might have questions about the changes and why they were made.

First, you'll probably need to get out of your log history by typing `q` in front of the `:` at the bottom of your shell. It will look something like this:  

```
commit 610e2a16ffca9665aabe9f58055f3b2bc64a4895
Author: Matt Langan <matt.langan@austintexas.gov>
Date:   Wed Jul 5 10:25:58 2017 -0500

    wip workflow
:
```

Now that you're back in your command prompt you need to tell Git 2 things:

1. You want to perform an _interactive rebase_
2. How far back in the history you want to go

The first step is handled by a simple Git command `$ git rebase -i`, and the second part is handled by appending additional context to that command. There are 2 ways to perform that second step.

If you know exactly which commit you want to go back to you can copy its hash and append it to the rebase command, so your whole command would look like:  

```
$ git rebase -i 610e2a16ffca9665aabe9f58055f3b2bc64a4895
```

That will tell Git that you're interested in rewriting the history starting at your most recent commit, going all the way back to the commit for the hash you provided.

The other option is simply tell Git that you want to go a set number of commits back from your latest commit. Let's say you only wanted to rewrite your most recent commit. In that case you would run:  
```
$ git rebase -i HEAD~1
```
Want to rewrite your last 7 commits?  
```
$ git rebase -i HEAD~7
```

## Performing the rebase

If your machine is properly configured then your default Git editor should open up a window that consists of your commit log at the top and rebase instructions at the bottom.

```
pick 6c6fd5e wip aggregate all guides outside of workflow
pick 13895ee wip unified guides
pick 7a22b65 wip local setup
pick 599a99f wip setup
pick 1b1db05 wip workflow

# Rebase 1b1db05..6c6fd5e onto e77065b (5 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

Note that the display order is the opposite from what you see when you run `$ git log`. The most recent commit is at the bottom, and the oldest is at the top.

It's critical that you treat this file with caution, as the work done here will be permanent. For example, if you delete one of the commit lines that commit will be lost. For this reason it is recommended that your local copy be pushed to the remote before performing the rebase. That way, if you make a mistake you can't recover from during the rebase, you can always delete your local feature branch, re-pull it from the remote, and start over.

### Rebase commands

You'll notice the list of commands available, starting with `pick` and ending with `drop`. By default, all of the commits are set to `pick` which, as you can see, simply tells Git to use the commit as-is. This retains the code change, the title, the commit body, and its order in the log. If you leave all actions as `pick` and close this window then the rebase will run and the history will not be changed.

Once you've selected your commands you need to save the file and close the window. If you're using Atom you need to close the the entire Atom application window. Once you've done that you should be redirected to your shell, where you will see messages from Git about its attempt to run your commands.

If the rebase fails or hits a conflict then you will see an error message. You can always run `$ git rebase —abort` to cancel the rebase and return to the commit history you had before attempting the rebase.

#### Reword (r)

The simplest change to make in a rebase is the `reword`. This lets you edit a commit's title and body, but makes no other changes to the history or code. To reword a commit, replace `pick` with `r` beside the commit hash.

When Git runs your `reword` command it will once again launch your default editor, this time with a file open for just that commit. Supply your commit title and message, then save and close the file to apply the commit. _Remember to insert an empty line between your title and commit body!_

Refer to [writing-a-commit.md](writing-a-commit.md) for guidelines on how to author your title and body.

As with the rebase log, if you're using Atom then both the file and application windows must be closed in order for Git to continue performing the rebase.

#### Fixup (f)

This is the command to use to combine multiple sets of changes into a single commit, while only retaining the commit title and message of the parent (top) commit. For example, if we applied the following changes to the rebase file...

```
pick 6c6fd5e wip aggregate all guides outside of workflow
f 13895ee wip unified guides
pick 7a22b65 wip local setup
pick 599a99f wip setup
pick 1b1db05 wip workflow
```

… then the _code_ changes in `13895ee` would be combined into the commit above it (`6c6fd5e`), and the commit title and body from `13895ee` would be destroyed. If that rebase were to be completed successfully then the next time you brought up the rebase window you would see

```
pick 6c6fd5e wip aggregate all guides outside of workflow
pick 7a22b65 wip local setup
pick 599a99f wip setup
pick 1b1db05 wip workflow
```

#### Drop (d)

This will remove the commit and your history will appear as though it was never created in the first place.

#### Combining commits that weren't made in succession

You can move lines around to change the order in which they will be reflected in the log. This is also useful when combined with a _fixup_. Let's take another look at our messy history and work through a reorder and fixup strategy. In this case, let's say that the we wanted to combine our most recent commit `1b1db05` with the first commit in our rebase history `6c6fd5e`.

Our original commit history looks like this:

```
pick 6c6fd5e wip aggregate all guides outside of workflow
pick 13895ee wip unified guides
pick 7a22b65 wip local setup
pick 599a99f wip setup
pick 1b1db05 wip workflow
```

First, we would move `pick 1b1db05 wip workflow` from line 5 to line 2, resulting in:

```
pick 6c6fd5e wip aggregate all guides outside of workflow
pick 1b1db05 wip workflow
pick 13895ee wip unified guides
pick 7a22b65 wip local setup
pick 599a99f wip setup
```

Next, we apply the `fixup` to the more recent commit in order to combine it with its intended parent commit:

```
pick 6c6fd5e wip aggregate all guides outside of workflow
f 1b1db05 wip workflow
pick 13895ee wip unified guides
pick 7a22b65 wip local setup
pick 599a99f wip setup
```

Now when we save and close the commit file Git will apply the code changes from `1b1db05` to `6c6fd5e`.