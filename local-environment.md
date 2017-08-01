# Configuring your local environment

Specific projects might have their own sets of required configurations, so the focus for this guide is on interoperability between remote GitHub repositories, your local Git configuration, and your code editor.

These instructions are focused on setting up a Mac OS X development environment.

If you need help configuring a Windows machine please [sign up for a developer training session](https://docs.google.com/forms/d/e/1FAIpQLSdeJtZzODlmgQEAaupbCoaekyXoCN32lk2ft0JWwLG5sewxhA/viewform?usp=sf_link).

## Download and install Atom

Atom is the lowest-common-denominator editor used by CoA web developers. It's lightweight, free, and is easy to set as your default Git editor. It's okay if you use a different editor for your daily work. This guide focuses on using Atom simply as your default Git editor. You are welcome to configure any editor you wish, but troubleshooting support will only be provided for Atom.  
Download and install Atom from [atom.io](https://atom.io)

## Download and install Git

You'll need Git installed on your system in order to do pretty much anything related to this workflow. This is not the GUI client, but instead a system-level installation that allows you to incorporate independent tools like Atom and Terminal to your workflow.  
Download at [https://git-scm.com/downloads](https://git-scm.com/downloads)

## Set Atom as your default Git editor

In order to adhere to the development process it is necessary to set a default Git editor. This makes it easy to compose thoughtful and exhaustive commit messages, which is a critical part of a sustainable and scalable development culture.

Again, you are welcome to configure any editor you wish, but the instructions below will focus on using Atom on your Windows or Mac machine.

Launch Terminal.app on your Mac and enter the following command:  

```
$ git config --global core.editor "atom --wait"
```

## Store your GitHub credentials so you don't have to provide them for every request

HTTPS is the recommended authentication method for your machine's communication with GitHub. To avoid having to re-enter your credentials for every request you can cache your GitHub credentials in the _credential helper_. [See the instructions on GitHub.com](https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac).

There is a sample repository you can use to trigger the initial authentication request. Here's how to use it:

1. **For GitHub.austintexas.gov**:  
   Clone the `authentication-testing` repository to your local projects directory  
   `$ git clone https://github.austintexas.gov/ctm-sandbox/authentication-testing.git`  
   **For GitHub.com:**  
   `$ git clone https://github.com/cityofaustin/authentication-testing.git`
2. Enter your email/username and password when prompted
3. TODO Add next steps by testing my own version

Make sure that you clone and initialize your repositories using the HTTPS URL rather than SSH.  
Example HTTPS URL: `https://github.com/cityofaustin/ctm-dev-workflow.git`  
Example SSH URL: `git@github.com:cityofaustin/ctm-dev-workflow.git`

If you prefer to use SSH you are welcome to do that instead of or in addition to HTTPS.

## Confirm that you did it all correctly

1. In your shell, `cd` to the `ctm-dev-workflow` project directory you cloned when storing your credentials

2. Add a new file called `test.md`

3. Stage your change for commit using `$ git add .`

4. Commit your change using `$ git commit`

5. Atom should open up a file called `COMMIT_EDITMSG`

6. Write a commit title in Line 1, such as "Test environment setup"

7. Write a commit body in Line 3 such as "This commit is for testing that all of my local setup was configured correctly"

8. Save the file and close the entire Atom window

9. You should be re-directed back to your shell window, which should display a note such as  

   ```
   1 file changed, 1 insertion(+), 0 deletion(-)
   ```

10. Run `$ git log` and confirm that the commit title and message you entered show up at the top of your shell window

11. Run `$ git push origin master`  
    If you see an error message that you do not have permissions then congratulations, everything's correct!  
    If you are prompted for your credentials again then something went wrong with your credential keychain. 

