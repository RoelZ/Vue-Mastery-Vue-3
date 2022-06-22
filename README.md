# real-world-vue
This repo is a fork of the [Vue Mastery course](https://www.vuemastery.com/courses/real-world-vue3), [Real World Vue 3 app](https://github.com/Code-Pop/Real-World_Vue-3).

## 8. Scaling the App
[![Scaling the App](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/images%2Fvideo-play-btn-small.png?alt=media&token=f455fef9-f9b9-461c-8cd6-69b98bec5909)](https://firebasestorage.googleapis.com/v0/b/gotvotes-71a47.appspot.com/o/videos%2F8.scaling-the-app.mp4?alt=media&token=cb7960ac-4a70-4ec6-9fdb-4a85e8193dff)  

## Scaling the app
We’ve reached the final lesson of this course, and I want to congratulate you for following along until the end. We’ve built a simple yet solid Vue app and deployed it out into the world. So where do we go from here? There are a number of features we could add, and additional concepts within the Vue framework (and ecosystem of tools) to learn. So what should a Vue developer master next?

In this lesson, I’m going to give a tour of what potential next steps we could take to scale up our app in different directions. This will simultaneously provide some guidance around how to continue with your Vue learning journey and how to best utilize the Vue Mastery platform to level up your skills.

## What’s next?
If you take a look at our courses page, you’ve probably already noticed we have our library of content arranged in different paths. These paths are arranged in the suggested order for consuming our courses. Having said that, your ideal next course ultimately depends on your current needs and pressing interests.

So let’s explore some of the main Vue concepts and additional tooling or frameworks you could add to your skillset.

## Vue 3 Forms
If we continued building out our Events for Good app beyond this course, we’d need a production-ready form that enables users to create new events. Forms are arguably one of the most important parts of any app, allowing us to intake important information from our users. A well done form (or a poorly done form) can ultimately affect a company’s bottom line in significant ways.

When building forms with Vue, you don’t just want to build a form that serves a specific purpose. You’ll want to know how to build a set of base form components that are highly reusable so they can be used and reused in a modular way throughout any of your Vue apps.

[Vuelidate](https://vuelidate-next.netlify.app/) is a well known plugin for Vue for makes handling user input much more easy.

Try to build it yourselve from the [documentation](https://vuelidate-next.netlify.app/guide.html) or when you liked this course, be sure to checkout the [Vue 3 Forms course from Vue Mastery](https://www.vuemastery.com/courses/vue3-forms/forms-introduction).

## Mastering Pinia (previously known as Vuex)
If we’ve implemented the ability for users to create new events, we’ll want a nice global location to store those events once they’re created. As our app’s component tree grows, it becomes increasing harder to manage the data within our app; as it’s created, updated, and displayed. This brings us to [Pinia](https://pinia.vuejs.org/): Vue’s current official library for state management.

As we've mentioned before, the Vue CLI is now in maintenance mode which can add Vuex to your project. Which (in theory) is the same as Pinia.

So when we created our project with the Vue CLI we selected Vuex. But what purpose, exactly, does it serve?

![](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F1.1609256665169.jpg?alt=media&token=e35761c1-2e17-4688-8006-4e532d1b0125)

As a Vue app grows, and you have more and more views and components within those views, you’ll need to have a reliable and predictable way to manage how that data is stored, sent around, and changed, within your app.

Notice how this store folder was installed into our project by the CLI. You can think of Vuex as the storage center for data throughout your app. Let’s look inside the store’s index.js:

📁 **store/index.js**

![](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F2.1609256888397.jpg?alt=media&token=f7724cd5-609b-4847-b097-6dd30809c799)

In short, the store provides us with what we need to keep track of the state of things within our app, and update that state in an organized modular way that is predictable and traceable.

Vue Mastery has a [Mastering Vuex course](https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex) that walks you through how to effectively use this state management library so things don’t get messy as you scale up your app’s data needs.
They also provide a [From Vuex to Pinia course](https://www.vuemastery.com/courses/from-vuex-to-pinia/what-is-pinia) to better understand the differences and how to implement it.

Please be aware that this course’s example app uses an earlier Vue 2 version of the app we built in this course. The reason we do not have a Vue 3 version of our Vuex course is because there has not been a major reworking of Vuex for Vue 3. The syntax for how Vuex is used and the concepts behind how it works are all the same whether you’re using Vue 2 or Vue 3. If you take the Mastering Vuex course and code along with it, I do suggest you use the example app from this Real World Vue 3 course and add the new Vuex features to it.

## Exploring Vite
Previously Webpack was the go-to bundler, but as the use of JavaScript projects grew into big ambiguous native/web applications, it would benefit a developer to have a more fast bundler process. This is why Vite came to life.

Not only does Vite run as a bundler, it can also be used as a scaffolding tool for your Vue, React, Svelte or Vanilla JavaScript apps, by using; 
```
npm create vite@latest my-vue-app -- --template vue
``` 

Don't throw Webpack away, just yet! But familiarize yourselve with the way Vite works for you in comparison to scaffolding your Vue app with the CLI and Webpack.

## Vue Router
While we covered the essentials of Vue Router in this course, I’ve mentioned how there are plenty more navigation-based abilities available to us with this handy routing library, and Vue Mastery's [Touring Vue Router course](https://www.vuemastery.com/courses/touring-vue-router/receiving-url-parameters) covers many of them.

![](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F3.1609256675823.jpg?alt=media&token=d1399229-46af-44fb-b2ef-e4666ebb8489)

So if your app needs features like pagination, guards on certain routes that limit user access, or if you need to enable programmatic navigation or nested routes, this course takes you beyond the essentials and tours various features within this routing toolset.

## Beyond the beginner’s path
If you take the courses outlined so far, you’ll have broadened and reinforced your knowledge of fundamental production-level Vue practices. You’ll then be ready for the [more intermediate courses](https://www.vuemastery.com/courses-path/advanced) that cover everything from strengthening your Vue apps with Unit Testing, to adding User Authentication, and integrating with popular libraries within the Vue.js ecosystem such as Nuxt.js and Vuetify.

## You’ve made it
With that, I hope you feel clear about what your next steps are on your path to Vue Mastery. I wish you well as you level up your skills and expand the opportunities that become available to you as you become increasingly skilled with this powerful JavaScript framework. See you in another course!

[<< Previous lesson](https://github.com/RoelZ/Vue-Mastery-Vue-3/tree/L7)