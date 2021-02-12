# Notes about git

## Procedures

### Start working with github.com
* please register to the website;
* please provide an ssh public key for every machine/account that you intend to use with git (see References). Please note that virtual machines should be registered as regular ones. In addition, please register the ssh public key also of the git for windows environment, if you use Git Bash.

### Start working on an existing project repo
* [github.com](http://github.com "github.com"): fork project (use web interface);
* set up a copy of the repo on your local machine by cloning your fork: `git clone <git_URL_of_your_fork>`;
Please make use of the `ssh` mechanism for cloning, such that you have also write rights when pushing to your fork;
* add the project repo as `remote upstream`: `git remote add upstream <git_URL_of_project_repo>`;
Please make use of the `https` mechanism, such that you don't have write rights and an accidental push to the project repo is hence rejected.

### Carry out your development
#### Initialise development
When you start your development, please create a suitable branch: `git checkout -b <my_devel_branch>`.

#### Regular activity
Whenever you have a set of changes that you want to keep trace of:
* check the status of your files:
	* `git status`: general overview of the status of the files;
	* `git diff`: show the modifications not yet `git add`-ed or `git commit`-ted;
* stage the relevant files for commit: `git add <all_the_relevant_files>`;
* actually commit files: `git commit` (please type in a sensible message, shortly explaining the content/goal of the changeset);
* propagate the changeset to your fork: `git push origin <my_devel_branch>`;

Nota Bene:
* if the diff on terminal is not colored, you can pipe the output of `git diff` to `colordiff`, a linux terminal utility that colors the diff, e.g. `git diff | colordiff`;
* `git status` and `git diff` can be run on single files: this is a convenient approach!

### Keep the local copy of your fork up-to-date
* commit all your relevant local changes: `git commit ...`;
* synchronise the `main` branch of your local copy of your fork against the `main` branch of the project repo:
	* checkout your main branch: `git checkout main`;
	* merge latest changes in project repo onto your local main: `git pull upstream main`.
	In case you want to be more cautious:
		* download latest changes from project repo (main branch) `git fetch upstream main`;
		* merge changes: `git merge upstream main`;
	* in case of conflicts:
		* solve them;
		* commit the merge: `git commit ...`;
	* propagate to github.com the update of your main branch: `git push origin main`;
* update your development branch:
	 * `git checkout <my_devel_branch>`;
	 * `git merge main`;
	 * in case of conflicts:
	 	* solve them;
	 	* `git commit ...`;
	 * `git push origin <my_devel_branch>`;

### Differences on terminal (ie on your local machine)
* differences between *two branches*: `git diff devel..main`
The command will show the differences between the `devel` and `main` branches, as if you were going to merge the `main` branch onto the `devel` one on your local machine.

### Pull Reuests (PRs)
Pull requests are changesets of code that should be merged on the project main branch.

#### How to create a PR
Please add me :)

#### How to accept a PR
Everything is done via the web interface on github.com:
* get a clue of what the PR is about: click on the PR to see the "Conversation" tab of the PR and go through the description of the PR. In case you can click on single commits;
* browse through the changes: click on the "Files Changed" tab to visualise files and add comments, in case. To add a comment, highlight the concerned lines, click on the "+" button that will be automatically opened and type in the message;
* add your final judgment to the PR ("revision"): from the "Files Changed" tab, click on "Review Changes", select the action that is appropriate and possibly leave a comment;
* in case the PR is ready for merging, merge it: go back to the "Conversation" tab and click on "Merge pull request".

## Git for Windows
git is also available for windows (see References for the download/manual page). The package comes with a windows GUI, for native Windows users, and a bash emulator, suitable for linux-minded users.

### Use ssh key in a non-default location
Especially with Git Bash, the ssh key is stored in an unconfortable path (e.g. `H`).
A key in a more sensible path can be generated, but should be loaded at every git operation implying communcation with the github.com server.
Here is an example:

```ssh-agent bash -c 'ssh-add <pathToPRIVATEkey> ; git push origin --delete add_converter'```

## References
* presentation by K. Sjobak ([slides](https://indico.cern.ch/event/439009/contributions/1927622/attachments/1156220/1662118/2015-09-15_SixTrack-GitHub.pdf "slides"));
* more on `git upstream`: [git docs](https://www.neonscience.org/resources/learning-hub/tutorials/git-setup-remote "git docs");
* generating an ssh public key: [git docs](https://git-scm.com/book/it/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key "git docs");
* [git for windows](https://gitforwindows.org/ "download page");
