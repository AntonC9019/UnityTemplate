Steps to setup a Unity repo:

1. Create a new repository from this repository (there's some "use template" button on github).

2. Make sure you have both `git` and `git-lfs` installed. If you're on mac, install these via Homebrew.
   ```
   brew install git
   brew install git-lfs
   ```

3. Clone the repository onto your computer. You can use a graphical tool like GitHub Desktop, or just do:
   ```
   git clone https://github.com/repo-user-name/repo-name
   ```
   When using git for the first time, however, it will require you to log in.
   As the username, type in your login from GitHub, and for the password you need to type in your access token.
   See [this](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) to find out how to create one (be sure to give it access to your repos, when creating).
   After that, configure your name and email in git in the terminal, otherwise it may hand forever while pushing commits.
   ```
   git config --global user.name YourGitHubNameHere
   git config --global user.email YourGitHubEmailHere
   ``` 

4. Run `git lfs install` in the root of the repo to make sure that Git LFS is enabled.
   
5. Add the unity folders into the project.
   You can check if Git LFS works correctly by showing the diff for a large file, like an FBX, in the console (first I'm staging it, then showing the diff):
   ```
   git add something.fbx
   git diff --cached something.fbx
   ```
      The output should be something like this:
   ```
   +version https://git-lfs.github.com/spec/v1
   +oid sha256:8f6717567b76aea297d723fe7725fe176105cd9bc29116aebfc6ff0afc4f929b
   +size 56646
   ```
   You can also check if it works in GitHub Desktop by clicking one of the changes and seeing the diff on the right.

5. Stage all added things. This command may take a while to process, because Unity projects can potentially have thousands of files.
   ```
   git add --all
   ```

6. Do the first commit. This will take even longer to process. I think, at this point Git LFS kicks in sending files to the server.
   ```
   git commit -m "Commit Unity files"
   ```

7. Commit the changes to the remote.
   ```
   git push
   ```


If you realize you've made a mistake, perhaps the Library folder did not get ignored, you can do a soft reset to a commit before you've added the files, and then modify your gitignore, after which you can stage your changes again:
```
# Show latest commits.
# Copy the hash of a working commit.
git log

# Go back to that commit without discarding changes.
# After this you can modify the gitignore.
git reset --soft commit-hash-you-copied

# Stage all files, do a commit
git add --all
git commit -m "Commmit project files"

# Rewrite the git history on the remote
git push --force-with-lease
```

At this point, it's important that other people who work with the repository, and still have the files that must have been ignored, do a fetch, and NOT commit the changes that they are shown.
Instead, they should do a hard reset to the remote's main branch:
```
# Get changes from the remote.
git fetch

# Reset to the remote's git history
git reset --hard origin/main 
```
