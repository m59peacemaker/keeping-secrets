# keeping secrets

> A strategy for keeping secrets from being committed with git.

There are several ways to keep secrets out your repo. What works best for you may depend on the environment you're working with and where your secrets are used. If you have a file that you don't want to git ignore, it contains secrets, and importing the secrets from another ignored file is not an option, this may be a good solution.

## ☠️ warning ☠️

I would still prefer to only publish this repo privately, where my purpose for keeping secrets out of it is for added security, or because I will be sharing it with colleagues. If the secrets should somehow end up published, you don't want that to be public!

### how things can go quite wrong:

- You forget to gitignore the secrets file. This is pretty bad. You do all this to remove secrets from all your profject files, but commit the file that has all the secrets. Don't do this.
- You forget to apply the filter to a project file that has secrets. It might be best to filter all files until a reason comes up to get more specific. `* filter=secrets`

## walkthrough

- add the scripts directory to your project
- make a secrets file template
  * optional, but maybe helpful for remembering what secrets need to be entered
- put your secrets in the project root in a file called `secrets`
  * use the typical linux conf format `KEY = VALUE` (spaces are optional)
- ignore the `secrets` file by adding it to `.gitignore`.
- wherever you need secrets in your project files, write `{KEY}`, replacing `KEY` with the actual key name of that secret, or write the secret itself
- assign the git filter, `secrets`, to files using the `.gitattributes` file
  * `* filter=secrets`
- execute the setup script
  * `$ ./scripts/git/setup`
  * this adds the `secrets` filter to the git project's config and runs the filter on your files for the first time
  * the secrets are now filled in where they belong, but will be reverted to placeholders when committing

## see if it works

- stage files that have secrets (`git add`) and then `git show :secrety-file` to check the contents.
- clone your project locally
  * `git clone your-project test-project`
- ensure that any files that had secrets have placeholders instead
- definitely make sure you didn't commit the `secrets` file, goof :)
