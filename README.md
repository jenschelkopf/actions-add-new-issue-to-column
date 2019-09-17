# Actions-AddNewIssueToColumn

### Demo

This demo shows a new issue called "Demo Issue" that automatically gets added to column in a project after being created.

All in all takes less than 30 seconds from the time the issue is created to the time a card is created for it in a project

![](demo.gif)

### Description

Github Action that is meant to automatically add a newly created issue to a specific column in a project. Example YAML workflow that will run whenever a new issue has been opened. The new issue that causes the workflow to run will be added to the specified column:

### YAML

```name: "New Issue Automation"
on:
  issues:
    types: [opened]
jobs:
  Add_New_Issue_To_Project:
    runs-on: ubuntu-latest
    steps:
    - uses: konradpabjan/actions-add-new-issue-to-column@aaa24960
      with:
        repo-token: "${{ secrets.GITHUB_TOKEN }}"
        project-url: "https://github.com/orgs/github/projects/1"
        column-name: "New issues should show up here"
 ```

If you are attempting to automatically move a new issue to a project that is in an org with a linked repository, you have to use a custom token that has repo access. You can add that as a secret under the settings and use that instead of `secrets.GITHUB_TOKEN`. The token that is normally passed in is only scoped to the repository and it doesn't have access to any projects that it may be linked to so it will fail with a `Resource not accessible by integration` error. If the project is setup at the org level (linked), it must also have `org:read` permissions.
