<center>Git notes</center>
===
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

In order not to call ssh-agent and not to add a key every time you start a new session - at the end of the ~ / .bashrc file, add:

# start ssh
{ eval $(ssh-agent -s) && ssh-add /home/user/.ssh/your_public_key; } &> /dev/null

If everything went well, then we will see: *Hi user-name! You've successfully authenticated, but GitHub does not provide shell access.*

***

After that we can push our new commits without using log and pas.

***


### <center>Creating a remote repository from the terminal</center> ###

***`curl -u 'user_name:password' https://api.github.com/user/repos -d '{"name":"wp1.loc", "description": "some description"}'`***

then:

***`git remote add origin git@github.com:user_name/repository_name.git`***

***

### <center>Current user</center> ###

Get current user:

***`git config user.name && git config user.email`***

Switch to the desired user:

***`git config user.name "user_name" && git config user.email "user@mail.com"`***

***

### <center>Change remote URL</center> ###

Run git remote to list the existing remotes and see their names and URLs:

git remote -v

git remote set-url git@github.com:alex-ismailov/Git-notes.git
