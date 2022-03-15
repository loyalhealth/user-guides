clickup test
# Loyal Hub Developer Guides
The files in this repository will be used to power the Developer Guides at https://hub.loyalhealth.com. API documentation is created automatically from the product APIs. This is a public repo and anyone can submit changes that will be reviewed by the Loyal team.

## Builder
To preview files, you can use the builder at https://hub.loyalhealth.com/builder. All eligible files from this repo will be listed in the dropdowns at the top of the page. Use the dropdowns to select a file to start editing or to use as a base. Clicking the `Preview` tab will show you how the file will be rendered inside Hub. Clicking the `Copy` button will copy the contents of the `Code` tab to your clipboard so that you can paste directly into GitHub or a local text editor. **Please note that the Builder does not save anything. If you refresh the page or navigate away, your changes will be lost. It only serves as a clipboard.**

## Editing files
You can edit, add, and delete files directly in GitHub. All edits will be done by creating branches and using pull requests. To edit, find a file and click the pencil icon. Make your changes (or post the copied code from Builder) and add a commit message. If this is the first change for a new branch, you will choose the "Create a new branch for this commit and start a pull request." option. If you are adding changes to an existing branch, choose the "Commit directly to the YOUR_BRANCH_NAME branch." option. And then click the Commit Changes button. If you want to make more changes to a branch, make sure to switch to that branch. You can switch branches by going to the main page and choosing your branch from the dropdown right above the directory of files.

To add a file, click the `Create New File` button from the main page. If you are adding a file to a previously created branch, make sure you've switched to that branch first. You will then commit your change to the appropriate branch. Make sure to use the `.md` file extension.

To delete a file, find that file and click the delete icon. And commit the change to the appropriate branch.

Once you are finished making changes, you will create a Pull Request. There are several places where you can do this. On the main page, there is a button next to the branch dropdown. Or you can go to the Pull Request tab (https://github.com/loyalhealth/user-guides/pulls). To create the Pull Request, make sure the master branch is selected on the left with your branch on the right and the arrow in the middle pointing to the master branch then click the `Create Pull Request` button.
![Pull Request Screenshot](/images/pull-request-screenshot.jpg "Pull Request Screenshot")

In order to be merged into master and displayed on the site, your Pull Request will need to be approved. Once you create the request, a reviewer will be notified. After its been reviewed and merged, it will be live on the site. However, some users might experience a delay of up to 24 hours because of cache.

Always create a new branch when making edits. This will help prevent stale branches and merge conflicts. Once your pull request has been merged, please delete that branch so they branches don't become overwhelming. As a general guideline, the preferred way of creating branches would be `GITHUB_USERNAME/FEATURE_OR_PULL_REQUEST_NAME`.

## Naming Structure
The files are shown in the Developer Guide based on how they are named in the repo. They are listed in alphabetical order and will be displayed that way on their app page in Hub. In order to better control the order, the files were prefixed with a number followed by an underscore. The names of the files were also camelcased. The original files were order by the hundreds (for example: `100_introduction.md` or `300_howDoIGetAKey.md`). The title of the file in the left sidebar is created by metadata added to the beginning of a file.
```md
---
name: Introduction
---

## Introduction
...rest of the file
```

If the metadata is not included, the title will created by removing the prefix, capitalizing the first letter and adding a space before each existing capital letter. For example, if there is no metadata, `300_howDoIGetAKey.md` would have a title of `How Do I Get A Key". It is highly recommended to add the metadata to the file for better control of the title.

## Images
If you want to include images, the image will need to be hosted somewhere and you will need to use an absolute path to the image. The easiest way to do this would be to them to the `images` directory in this repo. The absolute url would be `https://raw.githubusercontent.com/loyalhealth/user-guides/master/images/IMAGE_FILE_NAME.FILE_EXT`. **Please note that is path is referencing the master branch. The image will not be displayed until it has been pushed to master. When working with images, it might be beneficial to add them first and create a pull request prior to adding the image to a markdown file. Also, make sure to use the appropriate file extension for the image (.jpg, .png, etc)**

To include an image in a file, you use the following format:
```html
![IMAGE ALT TEXT](IMAGE_URL.FILE_EXT "IMAGE TITLE")
```

For example, the following would display the screenshot image from above:
```html
![Pull Request Screenshot](https://raw.githubusercontent.com/loyalhealth/user-guides/master/images/pull-request-screenshot.jpg "Pull Request Screenshot")
```

# Tips
I found https://www.markdownguide.org/cheat-sheet/ to be a decent mark down cheat sheet. 

Only the `basic`, `connect`, `empower` and `guide` directories will be published. Subdirectories are not currently supported. If you have a use case for that, let us know and we'll work for a solution.

When creating new files, I would recommend a prefix that is halfway between the place where you want to put it. This will help from having to rename file prefixes too often. For example, if you want to create a Dialog Builder page for Guide and have it show up between `200_chatbotInstallation.md` and `300_javascriptApi.md`, name it `250_dialogBuilder.md`.

