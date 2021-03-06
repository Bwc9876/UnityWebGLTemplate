# UnityWebGLTemplate

A template repo you can use to push your WebGL games to GitHub pages.  

Uses:
- [Unity Builder](https://github.com/marketplace/actions/unity-builder)
- [Unity License Activation](https://github.com/marketplace/actions/unity-request-activation-file)
- [Deploy to Pages](https://github.com/marketplace/actions/deploy-to-github-pages)  

[Example Repo](https://github.com/Bwc9876/UnityWebGL)

## How it Works

Whenever you merge a pull request, GitHub will automatically compile your game using Unity to WebGL, the resulting build files will then be pushed to the gh-pages branch.

## Setup

### Template Cloning

In the top right, select "Use this template", in the subsequent screen **ensure that you select "Include all branches"** or else the workflows won't work.  
  
![Clone the template](/images/clone-repo.png "Clone the template")

### Generating Project Files

Open Unity Hub, create a new project and set up whatever options you need to. Once the project is created close unity.  
Now open GitHub desktop, clone the repo into any folder.  
  
Copy the following folders from the Unity Project folder to the Git repo folder:
- ProjectSettings
- Assets
- Packages  
  
Once these are copied, delete the Unity Project folder and remove it from Unity Hub.  Finally, open the Git repo folder in UnityHub as a project.  

Now the unity project folder and the git repo folder have been merged successfully.  

### Versions  

First things first, you're going to want to go to [activate.yml](.github/workflows/activate.yml#L13) and edit "unityVersion" on line 13 to your target unity version.  
You're also going to want to do this in [main.yml](.github/workflows/main.yml#L44) on line 44.  

### License

Now, go to the "Actions" tab of this repo and select "Acquire activation file" in the left plane and click "Run workflow", then run it on the main branch. This will create a license request file as an artifact, to access this file click "Acquire Activation file" in the list of actions, and wait for the action to complete  
  
![Run Acquire activation action](/images/run-license-action.png "Run the action on the main branch")  
  
If all goes well, there should be an artifact available to download with the name Unity.your_unity_version.alf, download this file to your local machine.  
  
![Download artifact](/images/download-artifact.png "Look for Artifacts at the bottom")  
  
Once downloaded, head to https://license.unity3d.com/manual.  There, you will upload your .alf file, and retrieve a .ulf file. Now you need to go to the Settings tab of your repo, click on "Secrets" on the left, and add a secret named "UNITY_LICENSE" with the contents of your .ulf file. This will allow the unity builder action to run unity installations.  

After this step is done, it is safe to delete [activate.yml](.github/workflows/activate.yml)  
  
Changing versions will require you to repeat this step!  

## Important note about compression

GitHub pages does not allow for you to configure HTTP response headers for compression; so, you'll need to disable it in player settings.  
Head to `Edit > Project Settings > Player > Scroll down to "other settings" > Click the dropdown labelled "Compression Format" and select "Disabled"`.  
Also check the `Decompression Fallback` option.

## Try It Out

Now that your Unity license is setup, make a PR and merge it to your main branch, as long as the PR affects the game (stuff like the README and .gitignore won't trigger a build) the build action will start. Once the action finishes, open the page through the "deployments" section on the right side.
  
## Config

By default, unity builder won't run if the branch is 'dirty'. This means that you've directly edited the main branch and didn't use a Pull Request. to mitigate this, uncomment line 45 in [main.yml](.github/workflows/main.yml#L45).    
  
To enable the ability to build manually (without having to push), uncomment line 20 in [main.yml](.github/workflows/main.yml#L20).  

## Post-Setup

After setup you should delete this README file in favor of your own, the images folder can also be deleted.  

## Optional Steps

[Integrate With Discord](https://ardalis.com/integrate-github-and-discord-with-webhooks/)  
[Customize WebGL Template](https://docs.unity3d.com/Manual/webgl-templates.html)  
[Integrate a Testing Suite](https://game.ci/docs/github/test-runner)  
[Setup your own Runner for Faster Builds](https://docs.github.com/en/actions/hosting-your-own-runners/adding-self-hosted-runners)  
[Use a custom pull-request template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)  
[Use Git LFS (Edit your .gitattributes)](https://gist.github.com/webbertakken/ff250a0d5e59a8aae961c2e509c07fbc)  
[Add a Status Badge](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge)  
[Use a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) 
  
