# real-world-vue
This repo is a clone of the [Vue Mastery course](https://www.vuemastery.com/courses/real-world-vue3), [Real World Vue 3 app](https://github.com/Code-Pop/Real-World_Vue-3).

## 7. Deploying with Firebase

At this point, our example app has all of the features we need it to for this course. We’ve covered a lot of concepts along the way and unpacked fundamental Vue app development practices. We’re now ready to take our project to the next step of any real-world application and deploy it out into the real world. In this lesson, we’ll understand what happens in the build process and how to smoothly deploy our app with a convenient platform for this which is called Firebase.

## What happens when we build our app?
Before we deploy our Vue app, it has to first be built. If this concept is new to you, I’m referring to the process of compiling all of our code into a state that is ready to release onto the Internet for people to use.

Remember earlier in the course, when we learned how the **index.html** file is the “single page” of our single page application? We looked at how our App is being loaded into the `div` with the id of `"app"` in this file:

📁 **public/index.html**
```html
<div id="app"></div>
<!-- built files will be auto injected -->
```
Did you notice that below that div, there’s a comment telling us that when we build our app, the finished, deployable, built files will end up here? We can get a better grasp of what this looks like by running through the build process.

If we peek into our project’s package.json file, we’ll see these Vue CLI scripts available to us.

📄 **package.json**
```javascript
"scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  }
```
We’re already familiar with running the serve command in order to spin up our project on a local host. We’ve been using it throughout this course as we’ve developed the application code. Since we’re ready to take our project into the real world, we can move on to using the build command, which of course builds our project into a usable product that can be deployed. Let’s see what happens when we type the command npm run build in our terminal (while cd’d within the root of the project).

**Terminal**
```
$ npm run build

⠏  Building for production...

DONE  Compiled successfully in 9317ms         4:19:32 PM

File                                 Size            Gzipped

dist/js/chunk-vendors.3002c4a1.js    141.24 KiB      50.80 KiB
dist/js/app.f2213f62.js              5.08 KiB        1.98 KiB
dist/css/app.d5e424b2.css            0.61 KiB        0.38 KiB

Images and other types of assets omitted.

DONE  Build complete. The dist directory is ready to be deployed.
```

As we see, our app was compiled successfully and output into a new dist directory. This directory contains the production-ready code that we will deploy.

![](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1608049790199.jpg?alt=media&token=c81b9fb2-cb55-46a2-a77e-77d4a7bf8ead)

Taking a look inside this new dist directory, we’ll see a folder for our CSS code, another one full of our now-bundled JS code, and an index.html file. Sure enough, when we look inside that new, production-ready index.html, we see that our built files have been auto-injected, just like that comment promised.

📄 **dist/index.html**
```html
<div id=app></div>
<script src=/js/chunk-vendors.3002c4a1.js></script>
<script src=/js/app.f2213f62.js></script>
```
Now that we understand what this build process looks like, how do we actually go about deploying this code into production?

## A high-stakes headache
When talking about deployment, we’re actually talking about a rather complex and nuanced process.

To do it right, you’d need to:

1. Find a web hosting service responsible for serving your app
2. Hook up a custom domain for your site
3. Get SSL - https certificates to ensure you have a secure domain
4. Build the site locally, and drop those files into the server
5. Ensure everything is being served correctly

Once your app is deployed, there are additional concerns around maintaining it and continuing to deploy new and improved versions of it in a stable way, and ensuring you can roll back to earlier versions in an emergency. This can all be quite a pain. If you aren’t confident about what you’re doing, it’s a pretty high-stakes risk to take all of this on solo.

Fortunately, there are platforms that do a lot of the heavy lifting of deployment (and re-deployment) for us. Which brings me to my solution of choice, which we’ll be learning about in this lesson: [Google Firebase](https://firebase.google.com/).

![Google Firebase](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Fgoogle-firebase.png?alt=media&token=989ad4c7-982e-4c88-96fb-e4e63d3d9070)

## Firebase to the Rescue
Firebase provides a set of products and solutions, from which **Hosting** delivers instant deploys for your apps. You simply connect it up to your project’s repo, and it automatically builds and deploys your app onto a live site that users can see and interact with. It can also perform automatic updates for you so that whenever you push to your repo, Firebase automatically rebuilds and deploys your site with no additional work on your end.

![Firebase Solutions](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-solutions.png?alt=media&token=0c92bdb9-3884-4213-8c55-85970bcec937)

In order to get started using it to deploy our Vue app, you’ll just have to [hook up your Google Account](https://console.firebase.google.com/).


After you’ve completed the sign up [you’ll land on a dashboard](https://console.firebase.google.com/) where you can create your first project. 

![Add Firebase Project](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-add-project-step-1.png?alt=media&token=c91c8254-0c93-454f-8728-a9a7a3961627)

1. Create a new project by pressing **Add Project** and give your project a name.
2. Choose to enable or disable the use of Google Analytics.  
*for this current project it won't be useful, but it can be come in very handy!*

After your project has been created it will show you direct you to your **Project overview dashboard**.

As you may notice, there are a lot of products and services you could add to the project. In this case we only want to make use of Hosting, so click on **Hosting** and click **Get started**.

The setup will tell you to use the Firebase CLI by installing it on your local environment with NPM.

## Firebase CLI

Run the following command in your terminal.
```
npm install -g firebase-tools
```

When `firebase-tools` has been installed use the CLI to login into your Google account by running the following command.
```
firebase login
```

This will trigger a new browser which will ask you to connect the CLI with your Firebase account. This way, you can control Firebase functions from your terminal.


> ❗ **IMPORTANT:** In order to follow along with these steps, you’ll need to **clone** the Vue Mastery course repo to your personal Github account, if you haven't done so yet.

After the login has been completed, navigate to your project folder which we created in [Lesson 2](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L2) and run the following command.
```
firebase init
```

This will guide you through the steps you can take, depending on your choices.
We want to choose **Hosting: Configure files for Firebase Hosting and set up GitHub Action deploys**

![Firebase CLI init](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-cli-step-1.png?alt=media&token=3a34a411-caca-4da9-ba94-466e25c15f36)

Use the arrow keys and `<space>` key to select and press `<enter>`

### Project setup
The next step is where you can choose to `Use an existing project` and select the project you'd created earlier in your browser.

### Hosting

#### 1. What do you want to use as your public directory?
Firebase will ask you what you want to use as your public directory. It's important to know that we want to use our `/dist` folder, since our `/public` folder is only meant as a placeholder for our `index.html`, which will be used as a template when we run `npm run build`

So type `dist` and press `<enter>`

#### 2. Configure as a single-page app?
Press `y`, this will lead every route to our app. Since we handle everything with Vue, even the routes.

#### 3. Set up automatic builds and deploys with GitHub?
When choosing `Yes` the CLI will start a browser which will ask you to connect Firebase to your Github account.

- **For which GitHub repository would you like to set up a GitHub workflow? (format: user/repository)**  
After you'll be asked to state which repository should include a workflow. This will be our repo you forked, so normally `{your-github-username}/Vue-Mastery-Vue-3` if you haven't changed the project's name.

- **Set up the workflow to run a build script before every deploy?**  
Since we want to use an automatic deploy, it should have the latest files of our project.
So by adding `npm run build` to this workflow and Firebase uses the `dist` folder to deploy it to the hosting, we'll get the very latest version of our project.

  So press `y` and Firebase will ask what script should run.
The default `npm ci` (which means clean install) and `npm run build` should suffice for this project, so press `<enter>`

- **Set up automatic deployment to your site's live channel when a PR is merged?**  
With this option, Firebase deployment will be triggered from Github, when you push your latest code into a new Pull Request (PR) and merge this to a branch of your choice.

   Press `y`

- **What is the name of the GitHub branch associated with your site's live channel?**  
And here you state which branch you'll be using for merging your PR. This will be the `master` branch in our case.

**Congratulations!**  
You've just completed all the steps that are necessary for an automated deployment! Now we're going to check if it actually works.

## From development to live environment

As you may have noticed, after finishing the previous steps, Firebase created four new files in your codebase.

![Firebase project files](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-files.png?alt=media&token=27029d63-63bc-475e-840d-85be59906226)

These files contain all the information Github will need to setup an Action.

### Github
Now commit these files and push it to your repository.
As soon as you've pushed your files, be sure to check your new commit in Github. It will show an orange icon in front of the latest commit.

![Firebase project files](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-commit.png?alt=media&token=0c9e593f-1bf9-462b-b48e-5bfb6730f22c)

When you click on it you can see our new Deploy to Firebase Hosting is already being picked up by Github! If you'd like to see what's going on under the hood, you can click on details and see your build process being run in realtime.

![Firebase project files](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-github-action.png?alt=media&token=7567dbe7-c300-4404-bd33-240f97c95254)


With this part succesfully completed we now have two ways of automatically building and deploying our app.
1. When merging to the master branch
2. When creating a Pull Request from incoming changes, which will create preview url for you to share with other members of your project to verify.

### Firebase

If you head over to your Firebase console in the browser, check Hosting at the left side of your Project overview.

Here you'll notice that there's a custom domain created along with the release history of the published deployments.

![Firebase Hosting](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-hosting.png?alt=media&token=79289fd3-2883-4b95-8227-35a35ceecd88)

Now click on the domain link and see your Real World Vue app live on the web!

Remember, if in any case you want to roll back to a earlier version of a deployment of your app, you can do so in the **release history** on this page.
Every deployment will be shown in the list and you can roll back with one click.

## What’s next?
Now that we’ve finished coding our app and deployed it out into the wild, where do we go from here? There are many more features to add and concepts to unpack, and in our next lesson we’ll take a look at the different ways we can take this app to the next level. See you there!

[<< Previous lesson](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L6-start)
 | 
 [Next lesson >>](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L8)
