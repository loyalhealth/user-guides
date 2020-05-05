# Loyal Hub Developer Guides
The files in this repository will be used to power the Developer Guides at https://hub.loyalhealth.com. API documentation is created automatically from the product APIs. This is a public repo and anyone can submit changes that will be reviewed by the Loyal team.

## Builder
To preview files, you can use the builder at https://hub.loyalhealth.com/builder. All eligible files from this repo will be listed in the dropdowns at the top of the page. Use the dropdowns to select a file to start editing or to use as a base. Clicking the `Preview` tab will show you how the file will be rendered inside Hub. Clicking the `Copy` button will copy the contents of the `Code` tab to your clipboard so that you can paste directly into GitHub or a local text editor. **Please note that the Builder does not save anything. If you refresh the page or navigate away, your changes will be lost. It only serves as a clipboard.**

## Editing files
You can edit, add, and delete files directly in GitHub. All edits will be done by creating branches and using pull requests. To edit, find a file and click the pencil icon. Make your changes (or post the copied code from Builder) and add a commit message. If this is the first change for a new branch, you will choose the "Create a new branch for this commit and start a pull request." option. If you are adding changes to an existing branch, choose the "Commit directly to the YOUR_BRANCH_NAME branch." option. And then click the Commit Changes button. If you want to make more changes to a branch, make sure to switch to that branch. You can switch branches by going to the main page and choosing your branch from the dropdown right above the directory of files.

To add a file, click the `Create New File` button from the main page. If you are adding a file to a previously created branch, make sure you've switched to that branch first. You will then commit your change to the appropriate branch.

To delete a file, find that file and click the delete icon. And commit the change to the appropriate branch.

Once you are finished making changes, you will create a Pull Request. There are several places where you can do this. On the main page, there is a button next to the branch dropdown. Or you can go to the Pull Request tab (https://github.com/loyalhealth/user-guides/pulls). To create the Pull Request, make sure the master branch is selected on the left with your branch on the right and the arrow in the middle pointing to the master branch then click the `Create Pull Request` button.
![Pull Request Screenshot](/images/pull-request-screenshot.jpg "Pull Request Screenshot")

In order to be merged into master and displayed on the site, your Pull Request will need to be approved. Once you create the request, a reviewer will be notified. After its been reviewed and merged, it will be live on the site. However, some users might experience a delay of up to 24 hours because of cache.

## Tips
If you want to include images, the image will need to be hosted somewhere and you will need to use an absolute path to the image. The easiest way to do this would be to them to the `images` directory in this repo. The absolute url would be `https://raw.githubusercontent.com/loyalhealth/user-guides/master/images/IMAGE_FILE_NAME.FILE_EXT`. **Please note that is path is referencing the master branch. The image will not be displayed until it has been pushed to master. When working with images, it might be beneficial to add them first and create a pull request prior to adding the image to a markdown file. Also, make sure to use the appropriate file extension for the image (.jpg, .png, etc)**

To include an image in a file, you use the following format:
```html
![IMAGE ALT TEXT](IMAGE_URL.FILE_EXT "IMAGE TITLE")
```

For example, the following would display the screenshot image from above:
```html
![Pull Request Screenshot](https://raw.githubusercontent.com/loyalhealth/user-guides/master/images/pull-request-screenshot.jpg "Pull Request Screenshot")
```
