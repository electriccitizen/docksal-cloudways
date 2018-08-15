# [PROJECT]

Site URL: [URL]
Dashboard: [DASHBOARD]

[PROJECT] is a Composer-based Drupal 8 application hosted on [Cloudways](https://platform.cloudways.com). Follow this README to create your local environment, and to learn the best practices for effectively contributing to the project.

## Onboarding

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

```fin validate``` [(?)](docs/commands/VALIDATE.md)  to pull in changes from other team members and check your work against the upstream

```git push origin <your-feature-branch>``` to push your feature branch to Github if everything looks good

If you see errors or merge conflicts after running [fin sync](docs/commands/SYNC.md) or [fin validate](docs/commands/VALIDATE.md), you will need to work with the team to understand, fix, and commit the conflicting file(s) or other errors before continuing.

## Submit a Github pull request

When your work is ready and has passed any necessary QA. submit a Github pull request against your branch. A project maintainer will review the changes and merge into master.

**Important:** Any time a Github push occurs to the ```master``` branch (via a git push or a pull request), the code will be AUTOMATICALLY deployed to Cloudways. Once it is on Cloudways you will need to complete the additional steps below depending on the nature of your work. 

*Note: Advanced or otherwise approved users can submit and merge their own PRs, and/or merge and push a feature branch directly into master without a formal pull request. Ask if you have questions, err on the side of caution.*

## Post push 

After you push to ```master``` branch and your code is on Cloudways you will need to do several additional steps:

**Composer install**

If your changes included module updates, additions, or removals you will need to manually run ```composer install``` on the Cloudways server via SSH:

```ssh stemtc@178.128.150.228```

```composer install```

**Config import**

If your changes require a config import:

```drush @stemtc.prod cim```

**Database update**

If your module udpates or other changes require a database update:

```drush @stemtc.prod dbup```

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
