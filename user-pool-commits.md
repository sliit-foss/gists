# Make git commits from a user pool

## Description

- Makes things a little bit faster if you were to commit as multiple users to a single repository

## Prerequisites

- User should have git installed on their machine

## Steps to Setup

1. **Add the following bash script to the folder containing cloned repo. Recommended file name is 'cfup.sh':**

```bash
#!/bin/bash

message=$1
user=$2

configure_commit_push() {
   git config user.name "$1"
   git config user.email "$2"
   git add . && git commit -m "$message" && git push
}

# add more functions like below for additional users
talion() {
    configure_commit_push "Talion" "talion@gmail.com"
}

celebrimbor() {
    configure_commit_push "Celebrimbor" "celebrimbor@gmail.com"
}

shelob() {
    configure_commit_push "Shelob" "shelob@gmail.com>"
}

# add function names defining users to this array
functions=("talion" "celebrimbor" "shelob")

if [ -z "$user" ]; then
    random_function=${functions[$RANDOM % ${#functions[@]}]}
    $random_function
elif type "$user" >/dev/null 2>&1; then
    $user
else
    echo "Invalid user provided."
fi
```

1. **Replace functions user1,user2,user3 with functions calling configure_commit_push using the parameters of your users' configs. You can add any number of functions to suit the user count you wish. But remember to add those function names into functions array.**

## Usage

Refer [this](https://inpics.net/how-to-run-sh-file-on-linux-mac-windows/#:~:text=To%20run%20a%20bash%20script,%E2%80%9Cbash%20filename.sh%E2%80%9D.) to learn more about how to run bash scripts in different OSs. Given commands are for unix and linux.

2. **Commit and push as a random user from the pool (Replace cfup with your file name):**
    - sh cfup "chore: some commit message" - Commits and pushes as a random user from the pool

2. **Commit and push as user shelob (Replace cfup with your file name):**

    - sh cfup "chore: some commit message" shelob - Commits and pushes as user shelob

---
