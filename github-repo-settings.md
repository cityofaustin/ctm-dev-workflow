# Github repo settings

1. In current repo go to settings --> Collaborators & Teams. Under collaborators add the user `capdeploy`. Make sure capdeploy has write permissions
2. Next go to settings --> Hooks & services.
   - Under webhooks add `http://coacfbuild.austintexas.gov/github-webhook/` to payload url field and save settings.
   - Under services add the `Jenkins (Git Plugin)`. Add this url `http://coacfbuild.austintexas.gov/` to Jenkins url field. Save service.
