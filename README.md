# Application Development Workflow

This repo is a collaboration and publishing space for the CTM Application Development workflow. CoA software and web developers are encouraged to read the documentation and sign up for in-person training to learn how to incorporate the workflow into their daily work.

For now the guides will live here as markdown files but might evolve to be part of a broader documentation site, akin to [18F's Guides](https://guides.18f.gov).

## Getting Started

These are things that anyone doing software or web development at the CoA should have and know. The tools are free (or can be provided by the city) and the skills are easily learned. Training is available for anyone who would prefer 1-on-1 help getting ramped up. To request training see the "Support" section below.

### Familiarity/comfort with a command line interface

If you already know your `$ cd ..`s from your `$ sudo rm -rf`s then you can move ahead.

If you are not familiar with the command line, or if you want a refresher, then [sign up for a free codecademy account](https://www.codecademy.com/register) and take their [Learn the Command Line course](https://www.codecademy.com/learn/learn-the-command-line).

Mac users can use the built-in Terminal application that comes with OS X.

Windows users need to use something other than `Cmd.exe` since it is not a Unix shell. Git comes with a Unix shell that you can use.

### A city-supported code editor

If you already use one of the following editors then you're good to go. Otherwise, [download and install a free copy of Atom](https://atom.io).

- Coda
- Eclipse
- NetBeans
- Sublime
- TextMate
- Vim

### Git

Different from GitHub's desktop client, git runs at the system-level and allows you to invoke important git-specific commands from the shell.

[Download Git](https://git-scm.com/downloads).

## Support

The following support channels are available to help you:

- [Developer Training](https://docs.google.com/forms/d/e/1FAIpQLSdeJtZzODlmgQEAaupbCoaekyXoCN32lk2ft0JWwLG5sewxhA/viewform?usp=sf_link)  
  Fill out this form to request a training session at a time and location most convenient for you
- [Google Hangout Developer Help Desk](https://hangouts.google.com/hangouts/_/event/cff3pnftq7n1ov6ogch2a2hvld4?hl=en&authuser=0)  
  Join this Hangout to speak directly to someone who can help. Someone should be on-hand most of the time to answer questions, though sometimes me
- Slack #github channel<sup>1</sup>  
  Join fellow CoA developers and GitHub users in Slack to ask questions or see if someone else is facing the same problem you are. It's helpful for other developers to see what issues you're encountering, becuase maybe they've dealt with them as well or will have to deal with them in the future.
- Email  
  Email [Matt Langan](mailto:matt.langan@austintexas.gov) with questions

## Contributing

To contribute, follow the workflow prescribed in [workflow.md](workflow.md).
If you have questions or suggestions then create an Issue.

1. Make sure you are a Member of the GitHub.com CoA organization and a Contributor on this repo

2. Clone the repo
   ```
   $ git clone git@github.com:cityofaustin/ctm-dev-workflow.git
   ```


This repo just consists of markdown files, so no further setup guide is required. You can edit the static markdown files in your feature branch 

The documents are written with a formatting syntax called *markdown*, which is used by sites like Reddit, Trello, and SiteLeaf to allow content writers to invoke HTML elements using basic text characters.  GitHub and other hosting environments support a markdown superset called *kramdown* that allows for even greater utility. The [kramdown Quick Reference Guide](https://kramdown.gettalong.org/quickref.html) is a great starting point for familiarizing yourself with the syntax and its capabilities.

If you don't have a preferred markdown editor I recommend [Typora](https://typora.io) (Mac, Windows, Linux).

---

<sup>1</sup> *If you don't have a Slack account then send an email to [matt.langan@austintexas.gov](mailto:matt.langan@austinetxas.gov) to request one.*