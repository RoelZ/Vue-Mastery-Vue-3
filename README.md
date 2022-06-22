# real-world-vue

# real-world-vue
This repo is a fork of the [Vue Mastery course](https://www.vuemastery.com/courses/real-world-vue3), [Real World Vue 3 app](https://github.com/Code-Pop/Real-World_Vue-3).

## 7. Deploying with Firebase

**Important!** This branch is still WIP

## Deploying with Firebase
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

Run the following command in your terminal.
```
npm install -g firebase-tools
```

When `firebase-tools` has been installed use the CLI to login into your Google account by running the following command.
```
firebase login
```

This will trigger a new browser which will ask you to connect the CLI with your Firebase account. This way, you can control Firebase functions from your terminal.

After the login has been completed, navigate to your project folder which we created in [Lesson 2](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L2) and run the following command.
```
firebase init
```

This will guide you through the steps you can take, depending on your choices.
We want to choose **Hosting: Configure files for Firebase Hosting and set up GitHub Action deploys**

![Firebase CLI init](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2FL7%2Ffirebase-cli-step-1.png?alt=media&token=3a34a411-caca-4da9-ba94-466e25c15f36)

Use the arrow keys and `<space>` key to select and press `<enter>`

### Project setup
The next step is where you can choose to **Use an existing project** 
and choose the project you'd created earlier in your browser.

### What do you want to use as your public directory?
Firebase will ask you *What you want to use as your public directory?* It's important to know that we want to use our `/dist` folder, since our `/public` folder is mainly meant to place our `index.html` which will be used as a template when we run `npm run build`

So type `dist` and press `<enter>`

### Configure as a single-page app?
Press `y`, this will lead every route to our app. Since we handle everything with Vue, even the routes.

### Set up automatic builds and deploys with GitHub?

As you can see, we’re able to deploy a Static Site served over a global CDN with the ability to add a custom domain, plus SSL out of the box. If you’re not familiar, SSL (Secure Sockets Layer) is a protocol for web browsers and servers that allows for the authentication, encryption, and decryption of data sent over the Internet. In other words: it’s a built-in security measure that comes free with Render.

We’ll select this Static Site option to deploy our Vue app with Render, which prompts us to select a repo for the site that we want to deploy. Since we haven’t yet connected any repos to our Render account, we’ll click on the “Github” link to do so. If you’re not already logged into Github, you’ll sign in to install Render within your Github account and select the repo you’d like to connect.

❗IMPORTANT: In order to follow along with these steps, you’ll need to fork the Vue Mastery course repo to your personal Github account. That way, you’ll be able to connect the forked repo at this step.

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F6.1608050160184.jpg?alt=media&token=ab53f22d-2e2d-40b1-8182-2bb64884fc22

Upon clicking install, you’ll be redirected back to Render, where you should now see that newly connected repo showing up.

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F7.1608049833719.jpg?alt=media&token=3de82aa6-25ea-4faf-9e6b-c7655477e49d

Now we’re ready to select that repo and deploy it as a static site, which is a very straightforward process. As the page intelligently says: “You seem to be using Vue.js, so we’ve autofilled some fields accordingly.”

We’ll give our state site a Name; I’m calling it “Real World Vue 3”.

As for the Branch, this is where you’d typically select Master (which is the default selection) since most apps deploy the Master branch of their repo. However, in our case, since I’ve been building the app incrementally with each new lesson ending with its own ending branch, we’re going to select L6-end since this includes the final code for our entire example app.

We can leave the autofilled Build Command unchanged, as well as the name of the directory to publish to: dist (look familiar?).

There are additional Advanced options as well, including the ability to Add Environment Variables and/or a Secret File, but we’ll skip those for now.

I do want to bring your attention to the Auto Deploy field, though, which is set to “Yes” by default. This means our app will be automatically redeployed whenever a change is pushed to this branch, which is a pretty awesome feature. If we wanted to handle this manually, we’d toggle this to “No” and we could instead trigger a manual deploy with the button of the same name.

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F8.1608050183045.jpg?alt=media&token=fbafd2a8-12f8-4393-b5c4-d091d90b16f0

Now we’re ready to hit the Create Static Site button and watch Render bake our site into a delicious live site. 🥧

Adjusting for History Mode
We can now click on the link Render created for our site, which in my case is https://real-world-vue-3.onrender.com, to view our app live!

As we click around, it looks like it’s working. But watch what happens when we open a new tab and try going to a specific page, like: https://real-world-vue-3.onrender.com/event/123

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F9.1608049844886.jpg?alt=media&token=90cd89d2-7775-4810-924c-4e86bbe710d5

Uh oh… we’re getting a “Not Found” message, and there’s this 404 error in the console. Why is this happening?

In the Vue Router Essentials lesson, I briefly mentioned how our router is using history mode because we selected that option when we created our project from the Vue CLI. Well that just became very relevant.

📁src/router/index.js

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})
In history mode, our app is taking advantage of the browser’s history.pushState API to change the URL without reloading the page.

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F10.1608050201860.jpg?alt=media&token=e4165b7d-f18c-4031-a58b-ccdad9225ba5

The problem we’re currently running into is the fact that our app is a single page app, which means everything needs to be served from index.html. While our development server was configured to work this way for us, we need to configure Render’s rules so that it knows to always serve up index.html, no matter what url we navigate to.

We can do this very simply within the Redirect / Rewrite tab of our static site’s dashboard:

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F11.1608049857552.jpg?alt=media&token=6cd3f6b6-e897-4270-a605-0ff767e98b2a

We’ll add a catchall of /* and tell it to always Rewrite to /index.html Now, no matter what url we request, it will be served from index.html. Problem solved.

By the way… 🤔 If you’re wondering why everything seemed to work fine initially, before I pasted that url into a new tab and everything broke, that’s because when we first visited our new site, we visited the root route (’/’) which inherently served up index.html, and history mode took over from there.

With that catchall implemented, we’ve now solved our issue and successfully deployed our site. Before we end, let’s tour Render a bit more to understand what else is possible.

Touring Render
We already looked at the Redirects / Rewrites tab, but there are other tabs here that are just as useful, such as Events, which shows a history of deploys that have been made. This is where we can perform a rollback to a previous build if necessary.

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F12.1608050225404.jpg?alt=media&token=24ee1877-062f-45a2-b8d9-4384852c7e17

Under the Pull Request tab, you can enable pull requests and Render will automatically create a new instance of your site any time a pull request is created on your deployed branch. With its own URL, it can be used to review code before merging and will be deleted automatically when the PR is closed. This makes testing and collaboration easier.

Speaking of collaboration, you can also create and work within teams on Render, which an individual account holder can create from their dropdown here:

https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F13.1608050247646.jpg?alt=media&token=77eab61a-1198-4b23-a9a8-42d1ec71dd9d

Render scales with you
As your app scales, perhaps with a more robust backend or some server-side rendering, you can scale up your Render services, too—horizontally (add more instances of a service) or vertically (add more CPU and RAM to an instance)—with features including:

Web services
Managed PostgreSQL databases
Cron jobs
Private services
Background workers
And you can choose from several environments:

Docker
Node
Ruby
Go
Elixir
Python
Rust
A Helpful Community Forum
If you ever get stuck while using Render, they also have a community form that can help you get unstuck. In fact, they’ve even created a “Vue Mastery” category to address any issues you may run into while following this lesson.

## What’s next?
Now that we’ve finished coding our app and deployed it out into the wild, where do we go from here? There are many more features to add and concepts to unpack, and in our next lesson we’ll take a look at the different ways we can take this app to the next level. See you there!

[<< Previous lesson](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L6-start)
 | 
 [Next lesson >>](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L8)