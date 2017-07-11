# CitySpace

http://alpha.cityspace.austintexas.gov

CitySpace is the City of Austin employee intranet. It uses the Drupal 8 CMS and is deployed on Acquia Cloud using a Lightning distribution.

## Quick Start

### 1. Set up your Acquia Cloud account

1. Request an invitation to the CitySpace project on Acquia Cloud

2. Copy your SSH public key and add it to your Acquia Cloud account
   `$ pbcopy < ~/.ssh/id_rsa.pub` 

3. Confirm the SSH key is configured (you may have to wait several minutes for your key to propagate)

```
$ ssh austin1.test@staging-16599.prod.hosting.acquia.com

Your Hardware Enablement Stack (HWE) is supported until April 2017.

Welcome to Acquia Cloud. For information about shell access on this
server, please see: https://docs.acquia.com/acquia-cloud/ssh

Usage may be monitored and audited.

austin1@staging-16599:/mnt/gfs/home/austin1$ 

# Exit the shell

austin1@staging-16599:/mnt/gfs/home/austin1$ exit
logout
Connection to staging-16599.prod.hosting.acquia.com closed.Clone the Github repository
```

4. Request a Drupal Admin account on the Acquia server and follow the invitation instructions.
   *This step must be completed before you download the database and upload it to Dev Desktop*

### 2. Clone the repository

```
$ git clone git@github.com:cityofaustin/cityspace.git
```

### 3. Add Acquia as a remote

```
$ cd cityspace/
$ git remote add acquia austin1@svn-6135.prod.hosting.acquia.com:austin1.git
```

### 4. Install and configure local environment

1. Install dependencies
   We require several gems for CSS management. Use bundler to install them.

   ```
   # If you don't have bundler yet, install it
   $ gem install bundler

   # Once bundler is installed:
   $ cd docroot/themes/coa_intranet
   $ bundle install
   ```

2. Download and install Dev Desktop ("DD") from https://dev.acquia.com/downloads.

   1. Set "Desktop sites folder" to wherever you save your local projects
   2. After installation, deselect "Launch Acquia Dev Desktop" and click "Finish".
   3. Note that if you have an older version of Drush installed (for example, if you installed it as part of our work on the Drupal 7 AustinTexas.gov) you might need to unlink that older version of drush for this project.

3. Download [the drush aliases file](https://drive.google.com/file/d/0B-Jq2W8AQ6qOVXJ3U3JadXA3Q2M/view?usp=sharing) from Google Drive and move it to the `~/.drush/` directory.

   ```
   $ mv ~/PATH/TO/DOWNLOADED/austin1.aliases.drushrc.php ~/.drush/
   ```

4. Download the Acquia Cloud database to your Desktop.

   ```
   $ cd MY_PROJECT_DIRECTORY/
   $ drush @austin1.prod sql-dump > ~/Desktop/local.sql
   ```

   *You can specify a different destination path - The important thing is to download it outside of your project directory so that it does not get added to the git repository.*

5. Launch DevDesktop and select "Start with an existing Drupal site located on my computer".

   1. Set the "Local codebase folder" to the  `docroot/` directory in the CitySpace project.
   2. Set the "Local site name" to "austin1".
   3. Under the database dropdown select "Start with MySQL database dump file" and upload the `local.sql` file you downloaded earlier.

6. Ensure Dev Desktop is running (green lights next to "Apache" and "MySQL") and click on the "Local site" link to ensure your local server can serve the homepage.

7. Copy `docroot/sites/cofa.settings.local.php` to `docroot/sites/settings.local.php`

8. Sign In using the same credentials you established for your Drupal Admin account.

## Environments

Due to some tech and resourcing constraints, CitySpace is not configured for continuous integration. Supporing CI would require an additional layer of Drupal + Acquia configuration that we decided was not worth it during early development stages. In the future, however, this might be re-visited with our Acquia Technical Account Manager.

### Production

- **URL:** alpha.cityspace.austintexas.gov
- **Acquia:** [Prod](https://cloud.acquia.com/app/develop/applications/090d2f38-2e13-4b3a-8e5d-c460d582df43/environments/17643-090d2f38-2e13-4b3a-8e5d-c460d582df43)
- **GitHub:** `master`
- **Deployment:** Whenever somone accepts & merges a Pull Request (or batch of PRs) into `master` they should pull the updated branch onto their local machine and then manually initiate a deploy.

```
$ git checkout master
$ git pull
$ git push acquia master

# Run any drush scripts as necessary:
# (Must be in docroot/)
$ cd docroot/

# Apply updates to config database from yml files
$ drush @austin1.prod config-import active

# Apply any pending database and entity schema updates
$ drush @austin1.prod updb --entity-updates

# Clear cache
$ drush @austin1.prod cr
```

### Test

- **URL:** test.cityspace.austintexas.gov

- **Acquia:** [Test](https://cloud.acquia.com/app/develop/applications/090d2f38-2e13-4b3a-8e5d-c460d582df43/environments/17645-090d2f38-2e13-4b3a-8e5d-c460d582df43)

- **GitHub:** `test`

- **Description:** This is not meant to be a stable branch, but instead a way for developers to test their work in an environment that more closely matches `Prod`. As a result, it will be regularly destroyed and re-cloned from `master`.

  Before pushing to `Test` please confirm with the `#cityspace-dev` Slack channel that nobody else is actively using it to test their own feature branch(es).


The deployment process is similar to `Prod` but with a couple of exceptions.


- Use `austin1.test` instead of `austin1.prod` for your Drush command
- Push to `acquia test` rather than `acquia prod`
- Instead of PRing into `test` you might choose from 2 alternatives:
  - Rebase `my-feature` into `test` locally and deploy from test
  - Push my-feature _as_ test
    `$ git push acquia my-feature:test`
- You might need to do a force push if whatever was previously on `Test` is out-of-sync with the history in your feature branch
  `$ git push acquia test —force`
  ^ note that `force` is preceded by two dashes `-` `-`, which may appear in this doc as a single dash depending on what you're using to view this markdown file

### Local

- **URL:** [http://localhost/]() 

- **GitHub:** `mt-bonnell`

- **CSS workflow:** Our theme is based on the [U.S. Web Design Standards](https://github.com/18F/web-design-standards). The USWDS is implemented in [Sass](http://sass-lang.com/guide) and uses the [Bourbon](http://bourbon.io/) and [Neat](http://neat.bourbon.io/) libraries for mixins and grid, respectively.

  The various style specifications in `/docroot/themes/coa_intranet/assets/_scss` are aggregated by `styles.scss` and then compiled by [Compass](http://compass-style.org) into a single, minified stylesheet at `/docroot/themes/coa_intranet/assets/css/styles.css`. This file, as defined in [coa_intranet.libraries.yml](/docroot/themes/coa_intranet/coa_intranet.libraries.yml), gets served to the browser.

  In order to observe CSS changes in realtime you need to have Compass running in the background.

  ```
  $ cd docroot/themes/coa_intranet

  # Tell Compass to listen for changes to the Sass directory (specified in config.rb)
  $ compass watch
  >>> Compass is watching for changes. Press Ctrl-C to Stop.

  # Edit a file in the _scss/ directory, then save it. Any compile errors will be displayed here.
  >>> Compass is watching for changes. Press Ctrl-C to Stop.
   modified assets/_scss/cityspace/_overrides.scss
      write assets/css/styles.css
  ```

  Acquia Cloud does not support asset precompiling on the server, so assets must always be precompiled to `css/styles.css` before being deployed. This should not be a problem so long as you running the listener during your CSS development. However, if someone else has pushed an update to the precompiled `css/styles.css` you will almost certainly hit a merge conflict when you try to merge.

  #### Resolving a merge conflict on css/styles.css

  It's recommended that you _do not include styles.css_ in your commit and Pull Request. Instead, follow this workflow:

  1. Add and commit all of your `SASS` as you normally would, but do not include `css/styles.css`
  2. Get your feature branch merged into `master`
  3. Pull `master` into your local `master` and run `$ compass compile` in your SASS directory in order to force an update to the compiled CSS
  4. Add `css/styles.css` in a new commit titled "Precompile CSS" (no description required), and push that new commit directly back to `master`.

  > You: But Matt, we're NEVER supposed to commit directly to `master`! What gives?
  >
  > Matt: Yeah I know. It's the best I could think of. Sorry!

## Useful Drush commands

### Database
```
# Pull production database to test:
$ drush sql-sync -vv @austin1.prod @austin1.test

# Pull production database to local:
$ drush sql-sync -vv @austin1.prod @loc.austin1
```

### Assets
[Pull production files to test via Acquia](https://cloud.acquia.com/app/develop/applications/090d2f38-2e13-4b3a-8e5d-c460d582df43)
```
# Pull production files to local:
$ drush rsync @austin1.prod:%files sites/default/
```


### Deployment
```
Apply updates to config database from yml files
$ drush @austin1.prod config-import active

# Apply any pending database and entity schema updates
$ drush @austin1.prod updb --entity-updates

# Clear cache
$ drush @austin1.prod cr
```

### Modules
```
# Enables downloaded module if found, otherwise prompts to allow download of the latest recommended version & dependencies
$ drush en [module]

# Uninstall module
$ drush pmu [module]
```

## Contributing

Follow the workflow. Do your work in a feature branch, open a PR for review by the team, and make sure your commit history is clean and deliberate before considering your branch ready for merge.