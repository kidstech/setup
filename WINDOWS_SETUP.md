# Setting up the 3601 development environment (from 2021, like what we use for the Word River project) on Windows

This guide assumes you are running 64-bit Windows 10 or 11.

The simple list of what you need is:
- [Chrome](https://www.google.com/chrome/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Git](https://git-scm.com/)
- [GitKraken](https://www.gitkraken.com/git-client)
- [OpenJDK](https://adoptopenjdk.net/)
- [MongoDB Community Server](https://www.mongodb.com/)
- [NodeJS](https://nodejs.org/)
- [Angular CLI](https://cli.angular.io/)

Some of these have gotchas you will want to look out for so we have provided a more detailed guide below.

## Install Chrome

Download and run the installer from [google.com/chrome](https://www.google.com/chrome/) if you don't already have it.

## Install Visual Studio Code

Download and run the installer from [code.visualstudio.com](https://code.visualstudio.com/Download)

We recommend enabling the two "Add "Open with Code" action to Windows Explorer..." options:

![ivqONx](https://github.com/kidstech/setup/assets/2751987/43451d20-adbf-4c22-bac4-17a10acb4639)

## Install Git

Download and run the installer from [git-scm.com](https://git-scm.com/download/win)

Install it with the default options, except for the two screens described below. 

You may want to turn off the "Windows Explorer integration" shown below:

![8ouuB4](https://github.com/kidstech/setup/assets/2751987/64f45f2d-95ba-4388-bbe2-979963aec6df)

You may want to have it use VS Code as the default editor:

![qmw8cK](https://github.com/kidstech/setup/assets/2751987/70cd7e35-6277-449c-a747-d2a955052901)

You may want to adjust the name used for the initial branch in new repositories (we use "main"):

![GitDefaultUseMain](https://github.com/kidstech/setup/assets/2751987/959c0426-d748-4d23-b0ca-f3285f3cfbb2)

## Install GitKraken

Download and run the installer from [gitkraken.com](https://www.gitkraken.com/download/windows64)

When GitKraken starts after installing, click "Sign in with GitHub" and sign into your GitHub account. Then it will bring you to a "Set Up Your Profile" screen. Enter your name and the email address you used for your GitHub account here so your commits will show up as yours.

## Install the JDK

You need JDK version 11. We recommend OpenJDK 11 (LTS) from AdoptOpenJDK.

If you already have a Java version less than 11 installed, please uninstall it before proceeding. You can check if you have Java installed and what version it is by running `java --version` in PowerShell.

Download and install it from [adoptopenjdk.net](https://adoptopenjdk.net/?variant=openjdk11&jvmVariant=hotspot)

Select "Other platforms and versions", and in the "Version" dropdown menu, choose "11 - LTS". Scroll to the Windows x64 option and get the JDK (not just the JRE). Selecting the ".msi" version allows you to choose some options including enabling setting the JAVA_HOME as described and shown next:

It is recommended that you enable the "Set JAVA_HOME variable" option in the installer:

![nitvbc](https://github.com/kidstech/setup/assets/2751987/d81862f7-6f84-4e40-bb3a-a7f67d1d7b62)

## Install MongoDB

Download and run the MongoDB Community Server installer from [mongodb.com](https://www.mongodb.com/try/download/community).

The "Complete" installation is recommended. Leave the defaults for everything. It may open MongoDB Compass after installation, you can just close it.

### Adding the MongoDB tools to the PATH

Search for "environment" and open "Edit the system environment variables"

![DiOWum](https://github.com/kidstech/setup/assets/2751987/16165a13-fb62-45ec-9248-9c309c0b76c6)

Click "Environment Variables..."

![h4g9za](https://github.com/kidstech/setup/assets/2751987/a0bf1f23-0d8a-4f29-bc33-1dcdbdd3c37c)

Select "Path" in the bottom "System variables" pane and click "Edit..."

![KAY0A7](https://github.com/kidstech/setup/assets/2751987/384e53dc-98c4-4f6d-bc9f-495fdc68e9d7)

Make sure nothing is selected, click "Browse..."

![bV4Mei](https://github.com/kidstech/setup/assets/2751987/5cc80a6c-01d4-4349-9add-be4bd878b283)

Select `C:\Program Files\MongoDB\Server\[version]\bin`, where `[version]` is replaced by the version of Mongo you installed (in my example it is version 4.4), then click "OK"

![image](https://user-images.githubusercontent.com/1300395/104500523-28a79180-55a4-11eb-9959-aa7730d7f289.png)


### Test your MongoDB install

After adding the tools to your path, open a new PowerShell window and run `mongod --version`. It should work without errors as and look similar to the screenshot below.

<img width="657" alt="mongodtest" src="https://github.com/kidstech/setup/assets/2751987/eb50a376-b38b-4868-a437-fbf4fcfe4165">

### Also install extra Database Tools

After version 4.4 of MongoDB, some of the tools we need were split out into a separate thing we also need:

![MongoDBTools](https://github.com/kidstech/setup/assets/2751987/4243340e-6e44-4fa7-9fab-4cc62c412659)

https://www.mongodb.com/docs/database-tools/installation/installation-windows/

AND we need Mongo Shell (mongosh)
https://www.mongodb.com/docs/mongodb-shell/install/

## Install NodeJS (and a Node Version Manager)

We use an older version of Node for this project because there are some incompatible dependencies that crop up in later versions of Node with these older versions of other tools. But, you might also want to ba able to try out other versions of Node or use other versions for other projects, so you probably want to download a Node version manager. To manage Node versions on a Windows computer, we can use Fast Node Manager (fnm). Install fnm using WinGet (WinGet is built in for Windows 11, but you may need to install it for older versions of Windows) by running this in PowerShell:

```powershell
# installs fnm (Fast Node Manager)
winget install Schniz.fnm
```

We need to help Windows PowerShell know how to use fnm, and apparently there is no PowerShell profile by default. This [Stack Overflow Post](https://stackoverflow.com/questions/78522961/running-into-a-problem-installing-node-js-via-powershell-using-fnm) and this [documentation on the NodeJS site](https://nodejs.org/en/download/package-manager) helped form these directions:

Here is how to set up the PowerShell profile:

1. First, check that your profile does not exist. In PowerShell, run:
   ```powershell
   notepad $profile
   ```
   If Notepad cannot find the path, continue below, otherwise, jump to step 3.
2. Open PowerShell using admin access (you can do this from the Window Menu by start to type PowerShell and then selecting the option "Run as administrator") run:
   ```powershell
   if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }`
   ```
   to create the profile path forcefully. Restart PowerShell. 
3. Now we're gonna make sure PowerShell is able to run scripts. Open it and run: `Get-ExecutionPolicy -List`. If it says Restricted, then it won't run Node, or its associated env variables. So, to change it, open PowerShell in admin access (you can do this from the Window Menu by start to type PowerShell and then selecting the option "Run as administrator"), and use this code to change the restriction for [PowerShell execution policies](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4):
   ```powershell
   # not totally sure if both of these are needed or just LocalMachine, but this seemed to work
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```
4. Accept the change and restart PowerShell again. `Get-ExecutionPolicy -List` should show those changes have been applied.
5. Now, you should be able to open the Profile path by running: `notepad $PROFILE` (which should open a file that is currently empty). Append (add) the one line of code (script) mentioned in the fnm documentation, and save the file in NotePad: `fnm env --use-on-cd | Out-String | Invoke-Expression`.
6. Now you should be able to use fnm and node without issue:
   ```powershell
   # download and install Node.js (we want version 16 for this project)
   fnm use --install-if-missing 16
   
   # verifies the right Node.js version is in the environment
   node -v # should print `v16.20.2`
   
   # verifies the right NPM version is in the environment
   npm -v # should print `8.19.4`
   ```

If you ever need the most current version of Node (and you don't need to manage multiple versions of Node on your computer), you don't strictly need to use fnm to manage your Node installations. Instead, you can download and run the LTS Windows installer from [nodejs.org](https://nodejs.org/en/download/)

The "Tools for Native Modules" option is optional. It is not necessary for what we are doing but you may want it for future projects that need it.

![WA5jxL](https://github.com/kidstech/setup/assets/2751987/3707bbe2-1dbb-4ed6-8cd9-9c034ae4f4e6)


## Install the Angular CLI

For this project, we also need to use a pretty old version of the Angular Command Line Interface (CLI):

Open PowerShell and run
```powershell
npm install -g @angular/cli@11.2.3
```

Now try running `ng`. You will probably get this error:

![TOvNic](https://github.com/kidstech/setup/assets/2751987/160be244-3db0-4dd5-8734-cfca77e94a71)

To fix this run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Now if you run `ng` again you should get something like this:

![UHJyFS](https://github.com/kidstech/setup/assets/2751987/8dfa6cf5-d754-4c1f-ae15-1a248d8a7cd6)

## Additional Setup

We recommend you disable "Hide extensions for known file types" in "Files Explorer Options" so you can see the extensions of your files in Explorer.

You can just search for "File Explorer Options" and find the option in the "View" tab:

![jPuXlk](https://github.com/kidstech/setup/assets/2751987/fa27af08-9ae7-43fd-885b-f4c8cef995e3)

## Testing Out Your Setup

To test that everything is working:
1. Open GitKraken, click the `+` to open a tab, and click the button to "Clone a Repo".
2. There are multiple ways that will work, but these instructions will assume that you choose to "Clone with URL"
3. Choose the location on your computer for the local copy of your repository: In the "Where to clone to" textfield, browse to the location you'd like your Repo to go (usually a folder you will be able to locate later)
   ![CloneWithURL](https://github.com/kidstech/setup/assets/2751987/7583db7b-fa82-4334-8d7b-7653ba8ca10b)
4. Get the URL to put in the GitKraken URL textfield: In a Web browser like Chrome, go to the [Word River repository on GitHub](https://github.com/kidstech/word-river),
   ![GitHubCodeURL](https://github.com/kidstech/setup/assets/2751987/eb9bad58-eacc-461a-ac0b-cf0dd1ef4390)
   Click the green "Code" button, Copy the https URL to the clipboard, Paste into the URL textfield in GitKraken,
5. Clone the repository: Click "Clone the repo!"
   ![AfterPastingInURL](https://github.com/kidstech/setup/assets/2751987/766040a4-dc94-44eb-b7d9-fb2a822bc204)
6. Open the newly cloned repository: Immediately after you clone the repo, a message will probably show up that says "Successfully cloned repo 'word-river'" with "Open Now" and "OK" -- select "Open Now", which will look something like this (anytime you want to open a repo that has already been cloned, you just need to Open a Repo):
   ![OpenedInGitKraken](https://github.com/kidstech/setup/assets/2751987/6f92a387-77f9-468b-825e-fe8df2dce1e2)
7. Open VS Code
8. File > Open Folder (select the folder that is named word-river, which is the top-level folder of the project repo)
9. You may need to install some extensions that are suggested for this project
10. Make sure that Mongo is running and you are connected to Mongo (If you can't tell, try clicking on the extension icon on the left bar that looks like a leaf and see if the connection is showing up green like this)
   ![MongoConnected](https://github.com/kidstech/setup/assets/2751987/70d42afd-a657-413f-8dd2-9f64e2d6b95f)
If it's not, hover over the word "connection" and click the plus that appears (should bring up a view like this)
   ![MongoAddConnection](https://github.com/kidstech/setup/assets/2751987/0faed767-e4df-40c7-9914-20d4510a12c2)
Click on "Open Form" and without editing anything click on "Save & Connect"
11. Use VS Code's menu at the top of the screen to select "Terminal" and "New Terminal"
12. At the prompt in the terminal, type `cd database` and enter
13. At the prompt in the terminal, type `./mongoseed.bat` and enter
   This will "seed" the database (put some default values in the database). This runs a group or batch of commands and might also be called "running a batch file"
   ![SeedMongoDatabase](https://github.com/kidstech/setup/assets/2751987/a5e45a06-dca3-4cc2-9a7a-2a28a24b0b24)
14. Use VS Code's menu at the top of the screen to select "Terminal" and "New Terminal"
15. At the prompt in the terminal, type `cd server` and enter
16. At the prompt in the terminal, type `./gradlew run` and enter
   This will run the Javalin server (make our server ready to receive requests from the client) and it will look something like this while it is running (it stays at 75%, so don't let that throw you off)
17. To stop the server, use control-c and select Y to terminate the batch job. If you were going to use the server, you'd want to leave it running. You can open additional terminals. I usually like to have three going (one for the database, one for the server, and one for the client) in a split terminal so I can see what's happening in each.
18. At the prompt in the terminal, type `cd client` and enter
19. At the prompt in the terminal, type `npm install --legacy-peer-deps` and enter (this will take a while the first time and there will be lots of warnings:
   ![NpmInstallLegacy1](https://github.com/kidstech/setup/assets/2751987/64dda532-e2cf-4b5d-beac-17171e8e8ad0)
   ![NpmInstallLegacy2](https://github.com/kidstech/setup/assets/2751987/8e7e31b0-4631-482c-ab34-d506d71324f6)
20. In spite of those warnings and vulnerabilities, you can, indeed, run the client using `ng serve`
   ![NgServe1](https://github.com/kidstech/setup/assets/2751987/3618df4c-d5ee-4905-8f3b-579e8f9a647a)
   ![NgServe2](https://github.com/kidstech/setup/assets/2751987/3e0d40dc-9c36-42cd-8109-b489acbb1035)
21. Now, if you want to see the software in action, you can go back to the commands to run the server (`./gradlew run`) and run the client (`ng serve`),
   ![BothClientAndServerRunning](https://github.com/kidstech/setup/assets/2751987/a7feb0a7-9112-498a-b638-dc96dcb54ab8)
   and use Chrome or another web browser to see the app at http://localhost:4200
   ![WordRiverLocalHost](https://github.com/kidstech/setup/assets/2751987/f03a0ad6-55b1-494e-8df1-eed8eda73129)
