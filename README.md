# UnityWebGLTemplate

A template repo your can use to push your WebGL games to github pages

## Setup

### Versions  

First things first, you're going to want to go to [activate.yml](.github/workflows/activate.yml) and edit "unityVersion" on line 13 to your target unity version.  
Your also going to want to do this in [main.yml](.github/workflows/main.yml) on line 43.  
  
Changing versions will require you to repeat this step!

### License

Now, go to the "Actions" tab of this repo and select "Acquire activation file" in the left plane and click "Run workflow", the nrun it on the main branch. This will create a license request file as an artifact, to access this file click "Acquire Activation file" in the list of actions, and wait for the action to complete  
  
![Run Acquire activation action](/images/run-license-action.png "Run the action on the main branch")  
  
If all goes well, there should an artifact available to download with the name you.unity.version.alf, download this file to your local machine.  
  
![Download artifact](/images/download-artifact.png "Look for Artifacts at the bottom")  
  
Once downloaded, head to https://license.unity3d.com/manual.  There, you will upload your .alf file, and retrieve a .ulf file. Now you need to go to the Settings tab of your repo, click on "Secrets" on the right, and add a secret names "UNITY_LICENSE" with the contents of your .ulf file. This will allow the unity builder action to run unity installations.  

After this step is done, it is safe to delete [activate.yml](.github/workflows/activate.yml)

## Config

By default, unity builder won't run if the branch is 'dirty' this means that you've directly editted the main branch and didn't use a Pull Request. to mitigate this, uncomment line 44 in [main.yml](.github/workflows/main.yml).    
  
To enable the ability to build manually (without having to push), uncomment line 19 in [main.yml](.github/workflows/main.yml).  

## Post-Setup

After setup you should delete this README file in favor of your own, the images folder can also be deleted.  
