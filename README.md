Steps to setup:
1. Create a new repository from this repository (there's some "use template" button on github).

2. Make sure you have both `git` and `git-lfs` installed. If you're on mac, install these via Homebrew.
```
brew install git
brew install git-lfs
```

3. Clone the repository onto your computer. You can use a graphical tool like GitHub Desktop, or just do:
```
git clone link-to-repo
```

4. Add the unity folder into the project.
   I think you also need to run `git lfs install` in the root of the repo, though you can also check whether it is enabled by viewing the way that a large file, like an FBX, was commited (it should show you the hash of the file), which you can do in VSCode or GitHub Desktop by clicking on the diff of one of such FBX files.

5. Stage all added things. This command may take a while to process, because unity projects can potentially have thousands of files.
```
git add --all
```

6. Do the first commit. This will take even longer to process. I think, at this point Git LFS kicks in sending files to the server.
```
git commit -m "Commit Unity files"
```

7. Commit the changes to the remote. This one may hang forever on 100% completion, in which case you should check if the commit has appeared on the remote, and then you can safely kill it.
```
git push
```