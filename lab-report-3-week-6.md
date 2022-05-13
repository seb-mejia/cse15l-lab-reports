## Week 6 Lab Report
In this lab report, we will be using Windows as the operating system.

### Streamlining ssh Configuration
When logging into ssh, don't you find it tedious to enter the entire ieng6 email account?
Luckily...there's a shortcut to avoid entering that. I will demonstrate how to streamline your ssh configuration.

In File Explorer, change your directory so that you are in ~/.ssh/

When you enter this directory, you will need to access the "config" file.
If it doesn't exist, create a file named config (with no file extension).

![config pic](https://user-images.githubusercontent.com/90715607/167046311-3939f82c-8957-4a00-a684-142e5c10d9fc.PNG)

Now, you want to edit this config file. Here are the following steps to streamline your ssh configuration.
1. Double click the file
2. When prompted, open it in Notepad
3. Insert the following text in the file:
```
Host ieng6
    HostName ieng6.ucsd.edu
    User cs15lsp22zzz
```
*Note: zzz is your personal code*

In my case, the config file looks like this.

![configuration](https://user-images.githubusercontent.com/90715607/168382215-3d6b5a12-3fcf-4f07-85c2-12f9873327ef.PNG)

Afterwards, save the file and close it. Open Visual Studio code so we can access the server.

If done successfully, you should only have to enter ```ssh ieng6``` in the terminal to access the server.

![ssh](https://user-images.githubusercontent.com/90715607/167046709-9c0fb6eb-c8f1-495a-922a-f0618a55f997.PNG)

This shortcut makes it easier to use server-related commands, such as scp to transfer from your local repository to the server!

![scp](https://user-images.githubusercontent.com/90715607/167047640-0dc6bc36-a81e-47d1-9ee7-168891f16720.PNG)

### Setup Github Access from ieng6
Although the key that we just set up is pretty useful, we still need to give it some adjustments.
If you were to ```commit``` and ```push``` from the command line right now, you would get an error!

Remember in the first lab report when we made a public/private key pair to remotely access the ssh server?

If we want to set up Github access, we need to first find these keys.

To view your public key on the ssh servers, perform the following commands:
```
ls -al ~/.ssh
cat id_rsa.pub
```
This allows you to view the keypairs on the server. We are interested in the public key id_rsa.pub, which is why we use the `cat` command to view the contents of the key.

![public key](https://user-images.githubusercontent.com/90715607/167159626-88f34528-7cbd-467d-909e-73769116df3f.PNG)

We want to copy the contents of this key.

Next, to add this SSH key to your GitHub account, open the following link: https://github.com/settings/keys

Click "New SSH key", and create a new key with the content that you copied.

![SSH key](https://user-images.githubusercontent.com/90715607/167168928-3df9b89b-dd0b-4052-8a9c-53cad82f5cce.PNG)

I tested this key by creating a new repository named random-code with a file called HelloWorld.java.

If you were to git clone the repository (via SSH), you can edit the Java file via `vim HelloWorld.java`.

Once you've finished editing the file, use `git add` and `git commit -m"Reason goes here"`.

With this key set up, you should now be able to use `git push origin main`.

![git push origin main](https://user-images.githubusercontent.com/90715607/167169381-1eb80619-57dd-409d-9dfa-025fc866fb8d.PNG)

Woo-hoo!

Here is a link to the commit: https://github.com/TheSeb72/random-code/commit/1ff6eb30954273b8947dd4b249fef8c0c97555c1

### Copy whole directories with scp -r
Recently, we've been working with lots of files.
If you wanted to copy everything from markdown-parser to the ssh server, you COULD use scp for each individual file. But that would be really tedious.
What if, we could copy the entire directory to the server? Thankfully we can do this with recursive copying!

If we are in the markdown-parser directory of our local repository, we can copy this directory to the server with the following code:

`scp -r . ieng6:~/markdown-parser`

![recursive copy](https://user-images.githubusercontent.com/90715607/167171745-7228e192-7acc-4925-9071-a76c8d18dea6.PNG)

Some important notes:
* `-r` to recursively transfer files
* `.` the directory we want to copy (. refers to the current directory)
* `~/markdown-parser` the name of the new directory that we're copying to

Now, let's test these files by logging into the server and compiling/testing them.

![remote MarkdownParseTest](https://user-images.githubusercontent.com/90715607/167172926-05c41207-0a58-49e3-82d4-4042bb02bd39.PNG)

Looks pretty good! Our MarkdownParse and MarkdownParseTest files were both able to compile and run on the server successfully.

As we had done in week 1, we can combine `scp`, `;`, and `ssh` to copy our markdown-parser directory, and run it remotely in one line!

Using this code:
`scp -r . ieng6:~/markdown-parser; ssh ieng6 "cd markdown-parser; /software/CSE/oracle-java-17/jdk-17.0.1/bin/javac -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar MarkdownParseTest.java;/software/CSE/oracle-java-17/jdk-17.0.1/bin/java -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar org.junit.runner.JUnitCore MarkdownParseTest"`

![brainfuck](https://user-images.githubusercontent.com/90715607/167174832-c754664e-8ac0-4c11-b483-e6e5b4501da0.PNG)

Voila! I bet you feel like even MORE of a wizard now!
