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

Log into the server once again via `cs15lsp22XXX@ieng6.ucsd.edu`. If you enter `ls` in the terminal, you will see WhereAmI.java in the server's home directory. Success! While you're still logged into the server, use `javac WhereAmI.java` and `java WhereAmI` to run this file on the ieng6 computer. Notice anything different?

![FireShot Capture 006 - CSE15L Lab Team Nubian Goat - Google Docs - docs google com](https://user-images.githubusercontent.com/90715607/162535392-f41051ca-7360-4840-881f-172834c8de12.png)

**Step V. Setting an SSH Key**

Wow...this is so tedious and boring, right? If only there were a faster way to log into the server or run scp.

Guess what? `ssh` keys are here to make your life much easier!

These keys work thanks to a program called `ssh-keygen`, which creates a pair of files (public key and private key). The public key gets copied onto the server, while the private key is stored on the client (your computer). Once done, the `ssh` command will use this pair of files instead of your password.







Trash
![image](https://user-images.githubusercontent.com/90715607/162268012-9e693061-13d6-495c-ae77-f277c7b65577.png)
