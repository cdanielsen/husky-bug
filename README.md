Repo for testing possible bug reported at https://github.com/typicode/husky/issues/199

Steps to reproduce:
 - Clone the repo
 - Run `npm install`
 - Update index.js with a change that will violate a prettier rule (suggestion: add a new call to `sayHello` that is inented by two spaces)
 - Run `git add index.js` to stage your change
 - Run `git commit -m"attempting to commit code with a prettier error"`

Expected Result:
 - husky should invoke lint-staged via the `precommit` script
 - lint-staged should run tasks against index.js as it is captured by the `*.js` pattern
 - lint-staged should run the first task, invoking the prettier script, which should update index.js in place by removing the unecessary indentation
 - lint staged should run the second task, adding any updated files back to the staging area
 - lint staged should exit
 - index.js should be committed

 Actual Result:
  Husky prevents the commit with the message "npm run prettier -dd found some errors. Please fix them and try committing again"
  Additional npm error output due to `-dd` logging option that may or may not be relevant

 Note:
  Running `npm run precommit` produces the expected result
