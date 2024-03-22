
---

## GitHub Account Switching Method with Two Accounts

### Prerequisites:
- Install `gh` CLI tool from [GitHub CLI](https://cli.github.com/)

### Steps to Setup:

1. **Obtain PAT ( Personal access Token):**

    1. Click the profile icon on the top right corner.
    2. Navigate to developer settings.
    3. Select Personal Access Tokens and generate a token.

3. **Open `.gitconfig` File:**

   Navigate to the `.gitconfig` file inside your Users folder.

4. **Paste the Following Alias Configuration:**

   Add the following lines under the `[alias]` section in your `.gitconfig` file. Replace placeholders with valid values.

   ```ini
   [alias]
       control = "!f() { token='[PAT_Token_One]'; if [ $1 == "[first_trigger_name]" ]; then token='[PAT_Token_One]'; fi; echo $token | gh auth login --with-token; gh auth setup-git; }; f"
   ```
   Following is an example with dummy values,
    ```ini
    [alias]
        control = "!f() { token='iamtokenone'; if [ $1 == "[work]" ]; then token='iamtokentwo'; fi; echo $token | gh auth login --with-token; gh auth setup-git; }; f"
    ```

### Usage:

1. **Switching Between GitHub Accounts:**

   To switch between two GitHub accounts, use the provided alias `control` with a trigger name.

   ```bash
   git control [trigger_name_1]
   ```

   Replace `[trigger_name_1]` with your desired trigger name.

---
