# [PROJECT]

Site URL: [URL]

Dashboard: [DASHBOARD]

[PROJECT] is a Composer-based Drupal 8 application hosted on [Cloudways](https://platform.cloudways.com). Follow this README to create your local environment, and to learn the best practices for effectively contributing to the project.

## Onboarding

You'll need to make sure that you are on the Cloudways team and that you have added your public key to your account in order to SSH into the server. In the steps below, replace <youraccount>@ with your Cloudways username. For example, if your account name is ```adam``` then ```<youraccount>@178.128.150.228``` becomes:

```
ssh adam@178.128.150.228
```

Please remember: any time you commit to MASTER branch your code is automatically pushed directly to production. There is no “staging” server (at least for now). And then after that, you may need to manually login and run composer install if your changes require it. And of course you’ll need to run drush cim/drush updb/drush cr manually as needed, as none of this is automated.

This means there is no real way to get client approval on changes, short of screenshots on your local, and that you’ll need to be extra cautious about what you push up — it is what is, and the client seems to understand the risk/drawbacks in order to pay $20/mo instead of $125. Someday we will try to set up a proper staging server, but my first attempts were a mess and very difficult to push code between them.

If we ever DO have a change that needs to be reviewed by client or is too big we do have the capability of spinning up on-demand clones. You can also push your local branch and have it manually pulled and reviewed by a team member locally prior to merging into master, if necessary.

See the [setup documentation](docs/SETUP.md) if you are installing VirtualBox, Docksal, or Terminus for the first time. Once you meet the requirements, clone the this repository into your Docksal projects directory and initialize the site:

```cd ~/Projects```

```git clone git@github.com:electriccitizen/[SITE].git```

Move to your project's root folder and initialize the site:

```cd [SITE]```

```composer install```

```fin init```

Once the site is up, you are ready to start working:

* Local: http://[SITE].docksal
* Dev: http://dev-[SITE].pantheonsite.io
* User: admin/admin (local)

You typically only run [fin init](docs/commands/INIT.md) on your first-time setup, but can use it any time you want to reset or guarantee that your local environment is in a safe one-to-one state with your upstream environment.

Here are some other helpful ```fin``` commands that you will likely use in your day-to-day work:

```fin start``` to start your project services (or ```fin up``` if you need to re-load configuration for xdebug etc.)

```fin stop``` to stop your project services (recommended)

See (working with Docksal)[docs/local/DOCKSAL.md] for additional Docksal commands and tips.

See [troubleshooting Docksal](docs/local/TROUBLESHOOT.md) if things go bad.


## Recommended workflow

Here is a safe workflow that will help prevent lost work and other problems.

```fin sync``` [(?)](docs/commands/SYNC.md) to ensure your local site is synced with the upstream environment before starting a new task

```git checkout -b <your-feature-branch>``` to checkout a new feature branch and do your thing

```fin drush cex``` to export your changes

```git add``` to add any new configuration, theme, or custom module files

```git commit``` to commit your changes and get your feature branch into a safe, recoverable state

```fin validate``` [(?)](docs/commands/VALIDATE.md)  to pull in changes from other team members (master) and to check your work against the upstream

```git push origin <your-feature-branch>``` to push your feature branch to Github if everything looks good

If you see errors or merge conflicts after running [fin sync](docs/commands/SYNC.md) or [fin validate](docs/commands/VALIDATE.md), you will need to work with the team to understand, fix, and commit the conflicting file(s) or other errors before continuing.

## Submit a Github pull request

When your work is ready and has passed any necessary QA. submit a Github pull request against your branch. A project maintainer will review the changes and merge into master.

**Important:** Any time a Github push occurs to the ```master``` branch (via a git push or a pull request), the code will be AUTOMATICALLY deployed to the production Cloudways server. Once it is on Cloudways you will need to complete the additional steps below depending on the nature of your work.

*Note: Advanced or otherwise approved users can submit and merge their own PRs, and/or merge and push a feature branch directly into master without a formal pull request. Ask if you have questions, err on the side of caution.*

## Take a backup

If there is any risk your changes might break something it is wise to take an on-demand backup prior to pushing your changes to master. Login to Cloudways and:

```Servers > Stemtc > Backups > Take backup now```

## Post push

After you push to ```master``` branch and your code is on Cloudways, you may need to do several additional steps:

**Composer install**

If your changes included module updates, additions, or removals you will need to manually run ```composer install``` on the Cloudways server via SSH:

```ssh <youraccount>@178.128.150.228```

```composer install```

```exit```

**Config import**

If your changes require a config import:

```drush @stemtc.prod cim```

**Database update**

If your module udpates or other changes require a database update:

```drush @stemtc.prod dbup```

If you need a cache clear:

```drush @stemtc.prod cr```

 ## Be a good citizen

You are working in a team environment and must follow a few rules. If you are careless, it can lead to:

* Losing all of your uncommitted work (bad)
* Overriding or losing the work of others (worse)
* Uninstallable configuration or deploy errors

See this guide to [following a safe workflow](docs/workflow/WORKFLOW.md) when using configuration management in Drupal 8. The recommended workflow below follows these best practices, and includes two helper commands (```fin sync``` and ```fin validate```) that automate important components of a safe work flow.


## Next steps

These documents contain other important information about the project and working with your local environment.

* [Available commands](docs/commands/COMMANDS.md)
* [Following a safe workflow](docs/workflow/WORKFLOW.md)
* [Frontend and theming documentatiob](docs/frontend/THEME.md)
* [Project notes](docs/custom/NOTES.md)
* [Troubleshooting](docs/local/TROUBLESHOOT.md)
* [Working with Docksal](docs/local/DOCKSAL.md)

## Support and feedback

If you need support or find any errors or suggested improvements in this README contact <tim@electriccitizen.com>.

[Back to top](#[Project])

*<small>This is an auto-generated document. Keep any custom documents in the ```custom``` folder.</small>*
