(Personal use)
Lab 5 writeup: https://docs.google.com/document/d/17VpvLYf71mvpnjsJPhGfKCTBG9XWpWwpJpDk9NBpuiE/edit
Instructions page: https://docs.google.com/document/d/1u_IB3nJrXeve0HvcD1BNMa27yw6uMX4Jz7PXU_xIMP4/edit#

In this lab report, we will be using Windows as the operating system.

## Streamlining ssh Configuration
When logging into ssh, don't you find it tedious to enter the entire ieng6 email account?
Luckily...there's a shortcut to avoid entering that. I will demonstrate how to streamline your ssh configuration.

In File Explorer, change your directory so that you are in ~/.ssh/

When you enter this directory, there most likely won't be a file named "config".
Create a file named config, with no file extension.

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

Afterwards, save the file and close it. Open Visual Studio code so we can access the server.

If done successfully, you should only have to enter ```ssh ieng6``` in the terminal to access the server.

![ssh](https://user-images.githubusercontent.com/90715607/167046709-9c0fb6eb-c8f1-495a-922a-f0618a55f997.PNG)

This shortcut makes it easier to use server-related commands, such as scp to transfer from your local repository to the server!

![scp](https://user-images.githubusercontent.com/90715607/167047640-0dc6bc36-a81e-47d1-9ee7-168891f16720.PNG)

## Setup Github Access from ieng6
* Show where the public key you made is stored on Github and in your user account (screenshot).
* Show where the private key you made is stored on your user account (but not its contents) as a screenshot.
* Show running git commands to commit and push a change to Github while logged into your ieng6 account.
* Show a link for the resulting commit.

## Copy whole directories with scp -r
* Show copying your whole markdown-parse directory to your ieng6 account.
* Show logging into your ieng6 account after doing this and compiling and running the tests for your repository.
* Show (like in the last step of the first lab) combining scp, ;, and ssh to copy the whole directory and run the tests in one line.
