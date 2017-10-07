# First Timer Contributing

Never made an open source contribution before? Wondering how contributions work in the project? Here's a quick rundown!

* Find an issue that you are interested in addressing or a feature that you would like to add.
* Fork the repository associated with the issue to your local GitHub organization. This means that you will have a copy of the repository under `your-GitHub-username/repository-name`.
* Clone the repository to your local machine using `git clone https://github.com/sjones6/funcatron.git`.
* Create a new branch for your fix using `git checkout -b branch-name-here`.
* Make the appropriate changes for the issue you are trying to address or the feature that you want to add.
* Use `git add insert-paths-of-changed-files-here` to add the file contents of the changed files to the "snapshot" git uses to manage the state of the project, also known as the index.
* Use `git commit -m "Insert a short message of the changes made here"` to store the contents of the index with a descriptive message.
* Push the changes to the remote repository using `git push origin branch-name-here`.
* Submit a pull request to the main Funcatron repository. When you navigate to your forked branch in your Github profile, Github will usually prompt you if you have a branch with differences. But you can always navigate [here](https://github.com/sjones6/funcatron/pulls) to submit one as well.
* Title the pull request with a short description of the changes made and the issue or bug number associated with your change. For example, you can title an issue like so "Added more log outputting to resolve #4352".
* In the description of the pull request, explain the changes that you made, any issues you think exist with the pull request you made, and any questions you have for the maintainer. It's OK if your pull request is not perfect (no pull request is), the reviewer will be able to help you fix any problems and improve it!
* Wait for the pull request to be reviewed by a maintainer and approved.
* Make changes to the pull request if the reviewing maintainer recommends them.
* Celebrate your success after your pull request is merged!

## Next Steps

Check-out the [Code of Conduct](/code-of-conduct.md) and the [Guidelines](/contributing.md). Then, see if there are any [issues](https://github.com/sjones6/funcatron/issues) you want to tackle or [features](https://github.com/sjones6/funcatron/projects/1) you could work on!