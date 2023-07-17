# Github Authentication
You can authenticate to Github either by  HTTPS or SSH. However, authentication over HTTPS requires you to enter your `username` and `password` everytime you push your changes to remote repository. It's a repetative task and boring. To avoid using `username` and `password`, you can setup SSH key.

So, let's learn how to setup SSH key authentication and use it.

## SSH Key Generation and Setup

The following procedure explains how to generate SSH key in your machine and then saving it in your github account.

1. Open your terminal.
2. change your directory to root:
````
laptop@localhost:~ $ cd /
````

3. Run the follwoing command to generate a new SSH key:
```
laptop@localhost:/ $ ssh-keygen -t ed25519 -C "your_github_email_address"
````
Prompt will ask where to save the SSH key. Press `Enter` to accept the default location.

Next, prompt will ask to enter passphrase to secure the SSH key. Just press `Enter`. Again it will ask to enter the passphrase. Again you press `Enter`.

Output looks something like this:
````
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/username/.ssh/id_ed25519): 
Created directory '/home/username/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/username/.ssh/id_ed25519
Your public key has been saved in /home/username/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256: base encoded characters name@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|oo=+=   .o       |
| =*E=+ o. .      |
|..+&O...+        |
| ..=O+.  +       |
|   . .o.S        |
|  +    ..        |
| + o   o         |
|..o.  . .        |
|..o.+o           |
+----[SHA256]-----+
````

4. Start SSH-agent in the background:
````
laptop@localhost:/ $ eval "$(ssh-agent -s)"
````

output:
````
Agent pid 5463
````

**NOTE**: pid number is different for different machines. It may not be the same pid number when you start SSH-agent.

5. Add your SSH key to the SSH-agent:
````
laptop@localhost:/ $ ssh-add ~/.ssh/id_ed25519
````

output
````
Identity added: /home/username/.ssh/id_ed25519 (name@gmail.com)
````

6. Copy your SSH public key to your clipboard:
````
laptop@localhost:/ $ cat ~/.ssh/id_ed25519.pub
````

output:
````
you will see long sequence of encoded characters.
````

**IMPORTANT**: Select the complete string and do a right-click and copy it.

7. Now you have to add your SSH keys to your Github account. Login into your Github account and follow the steps mentioned below:

   a. Click your profile photo, then click **Settings**.

   b. On the left-navigation pane, click click  **SSH and GPG keys**.

   c. Click **New SSH key**.

   d. In the **Title" field**, add a descriptive for the new key.

   e. In the **Key** field, paste your public key which you copied from your terminal.

   f. Click **Add SSH key**.

   g. You will be asked to enter your password.

Now you have succesfully added SSH keys into your github account. Let's verify the SSH connection to ensure we have added the correct SSH keys into github account.

## Test SSH connection

1. On your terminal, enter the following:
````
laptop@localhost:/ $ ssh -T git@github.com
````

output
````
The authenticity of host 'github.com (IP ADDRESS)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Are you sure you want to continue connecting (yes/no)?
````

Enter `yes` to continue.

You get a msg like this:
````
Hi devops-guider! You've successfully authenticated, but GitHub does not provide shell access.
````

> Cheers! SSH Authentication is set and ready to use. Happy `Giting`.

