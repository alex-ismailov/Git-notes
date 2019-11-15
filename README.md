<h1 style="text-align: center">Git notes</h1>

### <center>ssh access to gihub</center> ###

**`ssh-keygen -t rsa -C "user@mail.com"`**

Enter passphrase to your SSH key(empty for no passphrase, but it is not recommended): * * *

Then git will ask in which directory to save the keys, if you specify only the file name, the keys will be saved in the working directory.

After that, two keys will appear in the directory you specify, one public for github, the second private, private key is stored on your computer.

***

Then check access:

**`ssh -T git@github.com`**

Permission denied (publickey).

At the current stage of configuring the ssh, this is normal since we have not yet placed the public key on the github.

In order to place a public key on a github, you need to add our public one in the account settings in the SSH and GPG keys section.

***

Run ssh-agent:

**`eval "$(ssh-agent -s)"`**

***

Add the key:

**`ssh-add /home/user/.ssh/<the name of your private key, which without extension>`**

Enter passphrase for /home/user/.ssh/<private key name>: ***

If everything went well, then we will see: *Identity added: /home/user/.ssh/< private key name > (/home/user/.ssh/< private key name >)*

***
Check:

**`ssh -T git@github.com`**

***

If everything went well, then we will see: *Hi user-name! You've successfully authenticated, but GitHub does not provide shell access.*

***

In order not to call ssh-agent and not to add a key every time you start a new session:

**`sudo apt install keychain`**

at the end of the ~ / .bashrc file, add:

**`# auto start ssh-agent`**

**`eval 'keychain --eval --agents ssh id_rsa'`**

** The private key must be called id_rsa otherwise keychain won't see it. I am looking for a solution**

After that the passphrase must be be entered only during the first login after a reboot.

Now we can push our new commits without using log and pas.

***

***


### <center>Creating a remote repository from the terminal</center> ###

***`curl -u 'user_name:password' https://api.github.com/user/repos -d '{"name":"repository_name", "description": "some description"}'`***

after:

if you are going to use ssh protocol:

***`git remote add origin git@github.com:user_name/repository_name.git`***

or

***`git remote add origin https://github.com/user_name/repository_name.git`***

if you are going to use https protocol.

***

### <center>Change remote URL</center> ###

Run git remote to list the existing remotes and see their names and URLs:

***`git remote -v`***

***`git remote set-url git@github.com:alex-ismailov/Git-notes.git`***

***

### <center>Remote tracking branches</center> ###

The tracked branch is directly linked to the branch on the remote repository. This allows you to reduce the sending of changes to the ***`git push`*** command without specifying parameters.

To push the current branch and set the remote as upstream, use:

***`git push --set-upstream origin master`***

After that you can find inforamtion about upstream branch is in the .git/config, in section  [branch "branch_name"]:

[branch "master"] <br/>
> remote = origin <br/>
> merge = refs/heads/master

***

### <center>Current user</center> ###

Get current user:

***`git config user.name && git config user.email`***

Switch to the desired user:

***`git config user.name "user_name" && git config user.email "user@mail.com"`***

***

### <center>Logs</center> ###

***`git log`***

***`git log --oneline --decorate --graph`***

***`git log --pretty=format:"%h - %an, %ar : %s"`***

***`git log --since=2.weeks`***

***`git log --since="120 minutes ago"`***

Output the last two logs: 

***`git log -2`***

or:

***`git log -p -2`***

***

### <center>Merge</center> ###

You have to make merge from that branch into which another branch will be filled.

***`git merge branch_name`***

### <center>Conflict resolution by kdiff3</center> ###

For conflict resolution you can use utility kdiff3

***`sudo apt install kdiff3`***

Latest git versions haves built-in support kdiff3, therefore there is no need to configure it manually.
So you only need to run:

***`git config --global merge.tool kdiff3`***

After that in \~/.gitconfig you will see new section:

[merge]<br>
> tool = kdiff3


Now to resolve conflict manually you need only run:

***`git mergetool`***