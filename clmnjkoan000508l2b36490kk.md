---
title: "What are preview URLs and why you should use them."
seoTitle: "You need to use Preview URLs today"
seoDescription: "Preview URLs using Vercel and Github for rapid testing."
datePublished: Sun Sep 17 2023 14:17:36 GMT+0000 (Coordinated Universal Time)
cuid: clmnjkoan000508l2b36490kk
slug: what-are-preview-urls-and-why-you-should-use-them
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694960106515/cf52356f-eeeb-4fa8-b41d-3ce86b87aecc.png
tags: github, javascript, devops, frontend-development, ci-cd

---

How does development happen in your organization? What is the journey your code takes from being pushed to your branch until it is deployed in production, ready to serve hundreds of millions of users?

### The usual process.

For most of you, the process is quite similar. You are likely to have a `main` or `master` branch on GitHub or another git source, and this main branch contains the code deployed on your production environment. When a developer begins working on a new feature, they create a feature branch from the main branch. Any code changes needed for the new feature are made in this feature branch. Once the developer has completed their changes, they create a pull request to merge the branch into the main branch. As soon as this occurs, a CI/CD pipeline or GitHub actions (more on that later) deploy the latest version of the main branch to production, and voilà, the new changes are live.

### The staging environment (The dress rehearsal)

Some (smarter) organizations maintain another environment called staging and it sits between the code in your feature branch and the live application in the production.

A staging environment is a simulated version of the production environment where developers, testers, and quality assurance teams can validate the application's functionality before it goes live. Think of it as the dress rehearsal before the main performance. In this controlled environment, software changes and updates are thoroughly tested to identify and rectify issues, ensuring that the final product is robust and reliable.

The staging environment is typically linked to a Git branch, often referred to as `development` or `staging` When a developer wants to work on a new feature, they create a branch from the staging branch. Once they have completed their changes, they submit a pull request to merge their updates into the staging branch.

On any given day, numerous developers may have their changes merged into the staging branch. In most organizations, a CI/CD pipeline is established, which is triggered as soon as this merge occurs. This pipeline deploys the changes to staging URLs, which the internal team can utilize for testing purposes.

### Introducing preview URLs

There are a few cases in which testing features as you develop them on a staging environment can be a pain.

1. In larger teams, when developers are working concurrently on numerous features, they all require access to the staging environment for testing their updates, which can lead to scarcity. There are solutions, such as maintaining individual stacks, but that is a complex topic best saved for another discussion.
    
2. At times, developers work on features that necessitate swift testing, pushing changes and testing them, then pushing additional updates and testing once more. This becomes challenging in a staging environment where other developers and testers depend on it too.
    
3. Rollback is difficult on a branch in which a lot of people are working simultaneously.
    

That is where preview deployment URLs come in handy. They provide temporary and easily shareable URLs and offer a way to view and interact with a specific version of a software application or website before it is deployed to a staging or production environment.

Preview URLs facilitate collaboration among team members and stakeholders, regardless of their physical location. Team members can share links to specific features or changes, making it easier to get feedback and input from colleagues, clients, or users.

Preview environments offer greater isolation and independence for different features or development branches. If a bug or issue arises in one preview environment, it does not affect other features being developed or tested in separate preview environments. This isolation helps maintain a high degree of agility and reduces the risk of feature conflicts.

### How to set up preview URLs using Vercel and GitHub.

Let's create an application and deploy it on Vercel. Next, we'll explore how preview URLs are generated automatically when you push updates to your feature branch.

Vercel is a cloud platform that specializes in modern web development. It provides a range of services and tools for deploying, hosting, and managing web applications, websites, and serverless functions. Vercel is designed to make web development and deployment faster, more accessible, and more efficient. Here are some key aspects of Vercel.

**Prerequisites**

1. **GitHub Repository:** You should have your project hosted on GitHub.
    
2. **Vercel Account:** Sign up for a Vercel account if you don't already have one at [**vercel.com**](http://vercel.com).
    

Create a simple ReactJS application using `create-react-app`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694956710284/e255b842-1d42-4421-8736-98c1c7d1d6e1.png align="center")

Create a GitHub repository for your project and push your changes to the main branch. Open your Vercel dashboard, click on the **Add New** button in the top right corner, and select **Project**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694956890172/7b41c384-7560-4637-be48-48ff3880b7d4.png align="center")

Next, you need to connect to your GitHub account. Vercel will prompt you to authorize access to your repositories using GitHub. Once you have granted access, choose the repository you created for your test project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694957033626/fa09d595-b2af-4866-969d-8878be114229.png align="center")

In the following step, you will input the build command and directory. Here, you should provide the command that Vercel can utilize to construct your React project, as well as the directory from which it can deploy the compiled application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694957075540/e87f162f-2e3d-4223-8570-7c677b8f03db.png align="center")

Click on deploy!

Open the Deployments tab in your Vercel project dashboard, where you will find a production deployment URL that Vercel has just generated for you.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694957369119/99a0ebff-5419-4220-8352-14171541254d.png align="center")

Open this and you should see the deployed react application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694957415457/1068a65f-5925-4b60-9ef0-c3d4b3840c0d.png align="center")

### Setting up a feature branch.

Go back to the terminal and create a branch `remove-logo` from the main branch of the project. We will now remove the React logo from the landing page. You can find it in `src/App.js`. Go ahead and delete it. Create a commit and push this new branch to the origin.

As soon as you push this, you can see another deployment running on the Vercel dashboard. Look how Vercel automatically recognized that it is a feature branch and tagged it as a `Preview`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694958986510/6cccc01e-0863-421e-8401-f3f67f9cc5b6.png align="center")

Once the deployment is complete, you can open it to find two URLs. The first URL, located at the top, will always contain the latest changes from your feature branch. The second URL is a temporary, one-time-use link created for the last change you pushed; this URL will change each time you push something new to your branch.

Open any of these URLs and you will see the preview of your latest change.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694959213948/4a65c246-2246-405c-96d2-fa0d7b4e2a67.png align="center")

Pretty Neat right?

Congratulations! You've successfully set up preview URLs with Vercel and GitHub, streamlining your development workflow and enabling efficient collaboration and testing before deploying changes to production.

---

> Follow me on [Twitter](https://twitter.com/devcodesthings) to stay updated with more articles like this. Subscribe to the newsletter below to get these right in your inbox as soon as I hit Publish!