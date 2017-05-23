# Jenkins workflow

1. Log into jenkins. http://coacfbuild.austintexas.gov/
2. Create new jenkins job using either `inside-template` or `external-template`.
3. Next, goto http://coacfiprod.austintexas.gov/jenkins_build/ to create the build.xml file. Once finished copy code and paste into a file called build.xml that is at the root of your application/directory
4. Commit code to repo under either ctm-ads-cfdevs or coldfusion-outside organization at github.austintexas.gov
5. In current repo go to settings --> Collaborators & Teams. Under collaborators add the user `capdeploy`. Make sure capdeploy has write permissions
6. Next go to settings --> Hooks & services.
   - Under webhooks add `http://coacfbuild.austintexas.gov/github-webhook/` to payload url field and save settings.
   - Under services add the `Jenkins (Git Plugin)`. Add this url `http://coacfbuild.austintexas.gov/` to Jenkins url field. Save service.
7. Add more code to your repo. When code is committed to repo's master branch, it should fire off job to move code from github.austintexas.gov to http://coacfdev.austintexas.gov/<folder-name>
