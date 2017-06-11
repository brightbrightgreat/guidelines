# General

## Table of Contents

1. [Process](#process)
2. [GitHub](#github)
2. [Tabs](#tabs)
3. [Grunt](#grunt)
4. [Icons](#icons)
5. [Help](#help)

## Process

You can find checklists to help guide each stage of the project [here](https://github.com/brightbrightgreat/skeleton/tree/master/lists). Be sure to check these often as you make progress.

If you are a contractor and/or not in BBG morning meetings, please check in with your project manager(s) once a week. To do so, send them an email every Friday with the following:

- Total hours worked on project so far
- How many hours did you use this week?
- Did you discover anything that might require additional hours beyond the original estimate?
- Are you on track to meet QA and launch deadlines?
- What did you work on this week? 
- What pieces do you plan to work on next week?
- Is anything holding you back? Are you waiting on assets/assistance/information from anyone?
- Do you have any concerns about the project?



## GitHub

Create a pull request as soon as you have enough code for others to start reviewing (~400 lines). Commit to the repo when modules/pages are ready for review, or at the end of every day, whichever comes first. Feel free to commit more often. 

Master branches are protected and will need administrator approval before a pull request can be merged in. Please pay attention to any request for changes administrators may make of you and address their concerns.

When working on a new project, you can do all your work on a branch called staging. 

When working on existing projects, make new branches for each feature/sprint. Name the branch descriptively but succinctly. Make it easy for others on the team to guess what the branch is for. Feature branches should be named feature/short-feature-name and bugfix branches should be named bugfix/short-bug-name. 

Be conscientious about referring to GitHub issues etc if relevant in your commit messages. 

Once a sprint is closed and the related branch successfully merged into master, you may delete the related branch. 

**Do not squash commits. Do not rebase unless you have discussed it with an admistrator first.** 

## Tabs
Hard tabs for indenting, spaces for alignment

## Grunt
We use Grunt for task running. You can find a Gruntfile.js and package.json file in the [Skeleton repo](https://github.com/brightbrightgreat/skeleton).

## Icons
Use SVG sprites for icons. The Grunt configurations found in the [Skeleton repo](https://github.com/brightbrightgreat/skeleton) includes SVG icon generation. 
The WordPress skeleton theme includes a function for easily calling icons from the icon sprite in the `functions.php` file (`bbg_get_icon()`).

## Help
If you have any questions, please contact Tiffany Stoik ([tiffany@brightbrightgreat.com](mailto:tiffany@brightbrightgreat.com)).
