# Adding New Icons

## Prerequisites
- A computer with a broadband internet connection (to clone a large repository)
- A terminal emulator program (you can use the default `Terminal.app`)
- A plain text editor or a special plist editor, such as the one built into Xcode or standalone options like [ProperTree](https://github.com/corpnewt/ProperTree) or [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/).
- A GitHub account ([https://github.com/join](https://github.com/join))
- Git with the git-lfs module
  - [How to install Git on any OS (github.com)](https://github.com/git-guides/install-git)
  - [Installing Git Large File Storage (docs.github.com)](https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage)
  - [Adding a new SSH key to your GitHub account (docs.github.com)](https://docs.github.com/en/github-ae@latest/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

## Steps

To add new icons to the repository and the website, follow these steps:

- Fork this repository.
- Clone the forked repository: `$ git clone git@github.com:<yourname>/legacy-mac-icons.github.io`
- Open the cloned repository: `$ cd legacy-mac-icons.github.io`

---

- Create a folder in the *`icons/<appname>`* directory.
**The folder name should be [alphanumeric](https://en.wikipedia.org/wiki/Alphanumericals) and NOT start with number.**
- Download an older version of the required application.
- Extract the **original** `.icns` file from the *`Contents/Resources`* folder inside your app `(Control + Click -> Show Package Contents)`.  
**YOU SHOULD NOT MODIFY THE ORIGINAL ICON IN ANY WAY, JUST GRAB THE FILE AND GO!!**
- Place the icon(s) into the *`icons/<appname>`* folder. **The icon filename should be [alphanumeric](https://en.wikipedia.org/wiki/Alphanumericals) and NOT start with number.**

---

- Copy the [example](example.info.plist) *`info.plist`* file into the *`icons/<appname>`* folder and open it with any plain text editor or use special plist editors like Xcode, ProperTree, PlistEdit Pro, etc.
- Make the following changes in the *`info.plist`* file:
  - Change `AddedBy` to your **name, nickname or GitHub username** (it will be shown on the website).
  - Change `AddedDate` to the current date in [ISO 8601](https://ru.wikipedia.org/wiki/ISO_8601) `YYYY-MM-DDThh:mm:ss±hh` format **(if you're using Xcode, change the key type to *Number* and then back to *Date* to populate the current system date)**.
  - In the `Application` section, change the following fields:
      - Insert into `Application -> AppPkgs` a new field with a **String** type.
      - Put potential paths to `.app` from the *`/Applications`* folder into it. For example, if the application should be in *`/Applications/Firefox.app`*, you can just set `Firefox.app`.  
      If the application is installed in a subfolder inside `/Applications`, like Adobe software or Xcode Developer Tools, you can set it like this: `Adobe Photoshop 2023/Adobe Photoshop 2023.app`, `Xcode.app/Contents/Developer/Applications/Simulator.app`.
      - If the default installation of the app is outside the *`/Applications`* folder, you should use a path that starts with `/` or `~/`, corresponding to the **boot drive root** and the **current user home directory**.  
     -  This information will be used by the *AutoIconReplacer* utility to auto-detect applications where icons can be changed.  
     - **A single app can have multiple paths for different versions!**
    - In `Application -> AppName`, insert the **official application name** *(or how they are displayed in Launchpad)*.
  - Next, go to the `Icons` section and create a new row with a type of **Dictionary**, and add the following fields:
      - `IconPath` is the path of the replacement icon in `.icns` format in the *`icons/<appname>`* directory of the main branch of the repository. It can be something like `./newicon.icns` or just `newicon.icns`. If the app has many variations of icons, you can use subfolders.
      - The `IconType` is the type of icon design. It can be:
          - `Flat` – for **post-Yosemite** icons (OS X 10.10 - 10.15).
          - `Skeuomorphic` – for **pre-Yosemite** icons (Mac OS X 10.0 - 10.9).
          - `Modern` – for **post-Big Sur** icons (macOS 11.0 to present).
      - You can also set additional comment for icon with `Comment` field. Like from which version this icon or something else.
  - Then create or go to the existing `Sources` section, which should be of type **Dictionary** and contain rows with a type of **String** with URLs of older versions that were used to extract icons. 
      - It is preferable to use **long-term sources** like [archive.org](https://archive.org/) or torrent trackers.  
      - **If you have no link, please reupload the app to archive.org instead of leaving it empty!**  
      - **DO NOT USE `Sources` section as the installation source for those apps. We do not verify the contents of it!**
- Now you can save your `info.plist` file.

---

![New folder summary](https://i.imgur.com/s6ZZscZ.png)
![Valid and populated info.plist](https://i.imgur.com/zl1q8C8.png)

- After ensuring that your folder looks like this and the `info.plist` contents are valid, you can add all the new files using `$ git add --all`.
- Commit the new changes using `$ git commit -m "Add new icons"`  
You can also specify for which apps the icons were added, like this: ``"Add new icons \`Application 1, Application 2\`"``
- Finally, push the changes into your fork using `$ git push` and open a pull request using the [New Icons template]().

---

If we find any issues with the `info.plist`, we will fix them ourselves and notify you.  
**You should not delete your fork until we have merged the changes!**

**P.S.** You can use the `$ plutil /path/to/info.plist` command in Terminal to check if the plist is valid.
