# Setting up the 3601 development environment on Windows

This guide assumes you are running 64-bit Windows 10.

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

https://www.mongodb.com/docs/database-tools/installation/installation-windows/


## Install NodeJS

Download and run the LTS Windows installer from [nodejs.org](https://nodejs.org/en/download/)

The "Tools for Native Modules" option is optional. It is not necessary for what we are doing but you may want it for future projects that need it.

![WA5jxL](https://github.com/kidstech/setup/assets/2751987/3707bbe2-1dbb-4ed6-8cd9-9c034ae4f4e6)


## Install the Angular CLI

Open PowerShell and run
```powershell
npm install -g @angular/cli
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
