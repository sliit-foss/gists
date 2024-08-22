# Changing author email of commits in bulk

Sometimes, you might need to update the author or committer information in Git commit history. This could be necessary if, for example, you've been using incorrect or outdated information.

Here's a step-by-step guide on how to rewrite commit history in Git to update author and committer information:

## Prerequisites

Before proceeding, make sure you have the following:

- Git installed on your system.
- Basic understanding of Git commands.

## Steps

1. **Identify the Incorrect Information:**


   Determine the incorrect author or committer information that needs to be updated. This typically includes the email address associated with the commits.


2. **Set up Variables:**

Replace "incorrect_email@example.com" with the incorrect email address, "new_author_name" with the desired new author name, and "new_email@example.com" with the desired new email address.

   ```bash
   WRONG_EMAIL="incorrect_email@example.com"
   NEW_NAME="new_author_name"
   NEW_EMAIL="new_email@example.com"
   ```
3. **Run the Command:**

Execute the following command in your Git repository:

   ```bash
WRONG_EMAIL=${1:-"user@gmail.com"}
NEW_NAME=${2:-"dinal-rock"}
NEW_EMAIL=${3:-"mrmihiraj@gmail.com"}

git filter-branch -f --env-filter "
if [ \"\$GIT_COMMITTER_EMAIL\" = \"$WRONG_EMAIL\" ]; then
  export GIT_COMMITTER_NAME=\"$NEW_NAME\"
  export GIT_COMMITTER_EMAIL=\"$NEW_EMAIL\"
fi
if [ \"\$GIT_AUTHOR_EMAIL\" = \"$WRONG_EMAIL\" ]; then
  export GIT_AUTHOR_NAME=\"$NEW_NAME\"
  export GIT_AUTHOR_EMAIL=\"$NEW_EMAIL\"
fi
" --tag-name-filter cat -- --branches --tags;
   ```

#### Explanation of the Command:

- `${1}`: Refers to the first argument passed to the script.
- `:-"default"`: Provides a default value if no argument is passed.

This means if you don't pass any arguments when running the script, it will use the default values provided. If you pass arguments, it will use those instead.
In this context if you run the script without any arguments, it will use the default values for the email and name. If you pass arguments, it will use those values instead.

- **`--env-filter`:** Specifies a filter to modify the environment (e.g., author and committer details) for each commit.
- **`--tag-name-filter cat`:** Ensures that tags are filtered but unchanged.
- **`-- --branches --tags`:** Specifies that all branches and tags should be rewritten.

For more detailed information about these flags, you can refer to the [Git filter-branch documentation](https://git-scm.com/docs/git-filter-branch).

4. **Verify Changes:**

After running the command, verify that the commit history has been updated correctly by checking a few commits.

5. **Push Changes (Optional):**

If you've made these changes in a repository that has already been pushed to a remote server, you'll need to force-push the changes:

```bash
git push --force
```

Note: Be cautious when force-pushing, as it can overwrite history for other collaborators.

6. **Conclusion**

Rewriting commit history can be useful for correcting inaccurate information. However, it's essential to use this command carefully, especially if you're working in a shared repository.

Always ensure you have a backup of your repository before performing any history rewriting operations.
