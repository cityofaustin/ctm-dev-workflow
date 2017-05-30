# Project Overview
CitySpace is the City of Austin employee intranet. It uses the Drupal 8 CMS and is deployed on Acquia Cloud using a Lightning distribution.

# Getting Started

### 1. Set up your Acquia Cloud account

1. Request an invitation to the CitySpace project on Acquia Cloud

2. Copy your SSH public key and add it to your Acquia Cloud account
   `$ pbcopy < ~/.ssh/id_rsa.pub` 

3. Confirm the SSH key is configured (you may have to wait several minutes for your key to propagate)

    ````
    $ ssh austin1.test@staging-16599.prod.hosting.acquia.com
    ````

   Your Hardware Enablement Stack (HWE) is supported until April 2017.

   Welcome to Acquia Cloud. For information about shell access on this
   server, please see: https://docs.acquia.com/acquia-cloud/ssh

   Usage may be monitored and audited.

   austin1@staging-16599:/mnt/gfs/home/austin1$ 

   # Exit the shell

   austin1@staging-16599:/mnt/gfs/home/austin1$ exit
   logout
   Connection to staging-16599.prod.hosting.acquia.com closed.Clone the Github repository
    ​````

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




# Contributing

### Dev Workflow

Our workflow is documented at [workflow.md](workflow.md)


### Legacy documentation

[https://github.austintexas.gov/ctm-webservices/cityspace_cloud/wiki](https://github.austintexas.gov/ctm-webservices/cityspace_cloud/wiki)