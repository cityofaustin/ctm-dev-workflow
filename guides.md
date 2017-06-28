# Application Development Guides

The following is a set of resources and instructions for CoA web developers to use in their daily work.

The full development workflow requires a number interdependent configurations among your local machine, GitHub accounts, and deployment environments. This ouline will take you through each of them in the order they need to be configured.

While the up-front overhead may be intimidating, it will be easy to develop good habits that will make the process feel seamless so long as you are dedicated to learning and instituting it in your daily work.

## Using the Command Line

If you already know your `$ cd ..`s from your `$ sudo rm -rf`s then you can move ahead. If you are not familiar with the command line, or if you want a refresher, then [sign up for a free codecademy account](https://www.codecademy.com/register) and take their [Learn the Command Line course](https://www.codecademy.com/learn/learn-the-command-line).

## Configuring your GitHub account

We use GitHub for version control, code review, and collaboration.  
**Reference:** [github.md](github.md)

## Configuring your local environment

Your system must be appropriately configured to take advantage of advanced Git features we will use.    
**Reference:** [local-environment.md](local-environment.md)

## Protecting your repository's `master` branch

There's only one rule about branches: anything in the `master` branch is _always_ deployable.  
**Reference:** [protected-branches.md](protected-branches.md)

## Creating a thorough README

A thoughtful and thorough `README` makes it easy for your peers to quickly understand how your application works and how to contribute to it. Start with [this template](README.md) and modify as appropriate for your project. This repository contains [a robust example](examples/alt-cityspace.md) from the CitySpace project for reference as you decide what to put into yours.

## Following the development workflow

The workflow instructs developers on how to apply the tools and processes listed in these guides to tell a logical and descriptive story about the code in the `master` branch.  
**Reference**: [workflow.md](workflow.md)