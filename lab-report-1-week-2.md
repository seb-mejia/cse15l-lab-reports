## Week 2 Lab Report

**Step I. Installing VS Code**

For this lab, we will assume that you are using a Windows computer. To install Visual Studio Code, visit [this website](https://code.visualstudio.com/) and click "Download" in the upper-right corner. Then, download the version corresponding to Windows. Once finished, your home page should look similar to the following image:

![image](https://user-images.githubusercontent.com/90715607/162271397-4a899b84-d223-45ad-8903-a2747bad4460.png)

**Step II. Remotely Connecting**

First, you will need to install a program called OpenSSH that will allow you to connect with other computers remotely.

[Instructions on downloading OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) (follow the steps in “Connect to a remote host”)

After you installed OpenSSH, open a terminal in VS Code. You can do this by clicking "Terminal" in the toolbar at the top, then selecting "New Terminal". In the terminal, input the following code:

`ssh cs15lsp22XXX@ieng6.ucsd.edu`

Note: XXX will be replaced by the letters in your CSE 15L specific account.

When you're logged in, you should be greeted with a screen resembling the one below:

![Screenshot (2216)](https://user-images.githubusercontent.com/90715607/162501484-3ca485d7-f8fa-4641-a0b3-0d538cf221be.png)

**Step III. Trying Some Commands**

Now that you've connected to the server, try out some Unix commands in the server! Here's a few useful ones to start with:

* ls: List files
* ls -a: List all files, including hidden files
* pwd: Print working directory
* mkdir: Make directory
* cp: Copy files and directories

![Screenshot (2219)](https://user-images.githubusercontent.com/90715607/162506667-9876706d-4f78-49d1-b270-503cf82f6466.png)

**Step IV. Moving Files with scp**

`scp` is a very important command! With this keyword, you are allowed to copy files from your computer to a remote server. You can only use this command while running on the client (i.e. your computer), it will not work while logged into ieng6.

Make a file on your computer called `WhereAmI.java` and fill it with the following code:

```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

After using `javac WhereAmI.java` to compile the file and `java WhereAmI` to run it, you should get relevant information for your computer.

![WhereAmI local](https://user-images.githubusercontent.com/90715607/162533785-5f66141a-9211-4e89-a60c-7e606e0e2092.png)

What if you tried opening this file from the server? Would you get the same information from the system?

Let's try it out with scp. In the terminal, type in `scp WhereAmI.java cs15lsp22XXX@ieng6.ucsd.edu` (replacing XXX with your course-specific username). You will then get confirmation that your file was transferred to the server.

![(Special Containment Procedures)](https://user-images.githubusercontent.com/90715607/162534605-d2638149-47c5-4b89-a2b4-6421c9d842d7.png)

Log into the server once again via `ssh cs15lsp22XXX@ieng6.ucsd.edu`. If you enter `ls` in the terminal, you will see WhereAmI.java in the server's home directory. Success! While you're still logged into the server, use `javac WhereAmI.java` and `java WhereAmI` to run this file on the ieng6 computer. Notice anything different?

![FireShot Capture 006 - CSE15L Lab Team Nubian Goat - Google Docs - docs google com](https://user-images.githubusercontent.com/90715607/162535392-f41051ca-7360-4840-881f-172834c8de12.png)

If done correctly, you should get different information related to the server itself.

**Step V. Setting an SSH Key**

Wow...copy-pasing the password is so tedious and boring, right? If only there were a faster way to log into the server or run scp.

Guess what? `ssh` keys are here to make your life much easier!

These keys work thanks to a program called `ssh-keygen`, which creates a pair of files (public key and private key). The public key gets copied onto the server, while the private key is stored on the client (your computer). Once done, the `ssh` command will use this pair of files instead of your password.

Enter `ssh-keygen` into the terminal. When asked which file to save the key in, enter `C:\Users\ZZZ/.ssh/id_rsa`.

You will be prompted to enter a passphrase. Do NOT enter a passphrase.

![Capture](https://user-images.githubusercontent.com/90715607/162536456-f49119b7-d938-4b3e-ac8d-1023e51e584c.PNG)

The program will then create a private key (in a file `id_rsa`) and public key (in a file `id_rsa.pub`) stored in the `.ssh` directory on your computer.

Recall that the private key is meant to be stored on your computer. However, we need to transfer the public key to the server. Let's move this file to the `.ssh` directory of your account on the server.

Log into the server, and use `mkdir .ssh` to make the .ssh directory on the server. This will either create the directory, or you will get a message that it already exists.

Afterwards, log out of the server. Now that you're back on the client, enter the following command.

`scp /Users/ZZZ/.ssh/id_rsa.pub cs15lsp22XXX@ieng6.ucsd.edu:~/.ssh/authorized_keys`

Note: ZZZ and XXX should be replaced by your computer username and your CSE 15L account username respectively.

After completing these steps, you will be able to use `ssh` and `scp` without entering your password.

![Capture1](https://user-images.githubusercontent.com/90715607/162630381-613f1ccb-0e07-4db8-9e68-3211c1c50bec.PNG)

**Step VI. Optimizing Remote Running**

But we can go even farther, right?

Let's think of how we can use what we've learned to locally edit `WhereAmI.java`, then copy it to the server, and finally run it.

* First, edit the file on your client as needed.
* Next, thanks to SSH keys, simply entering `ssh cs15lsp22XXX@ieng6.ucsd.edu` will log you into the server.
* Then, you want to send WhereAmI.java to the server with `scp`.
* You will want to compile the file with `javac` before running it.
* Finally, you can run the file with `java`.

Still too overwhelming? We can condense the process by using semicolons and quotation marks.

After writing down `ssh`, you can use quotes to directly run a command on the remote server. If you wanted to transfer a file to a server right after logging into it, you would include `scp` on the same line like so: `ssh cs15lsp22XXX@ieng6.ucsd.edu "scp [...]"`

In addition, you can use the semicolon to run multiple commands at the same time. If you want to compile WhereAmI.java AND run it on the same line, you would do the following: `javac WhereAmI.java; java WhereAmI`

With that said, you need two steps to complete the pocess.
1. Make a change to WhereAmI.java, then save the file.
2. Enter in the terminal: `ssh cs15lsp22XXX@ieng6.ucsd.edu "scp WhereAmI.java cs15lsp22XXX@ieng6.ucsd.edu; javac WhereAmI.java; java WhereAmI"`

![Screenshot (2235)](https://user-images.githubusercontent.com/90715607/162645615-7954c19c-b605-43e5-a0d2-20997b6a46f1.png)

Voilla! Don't you feel like a wizard?
