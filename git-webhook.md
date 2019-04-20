*Standard/Successful Branching Model :  Stable Master Branches and Tag Model.


Difference between Git merge --no-ff and git merge plain

The --no-ff flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature. Compare:

In the latter case, it is impossible to see from the Git history which of the commit objects together have implemented a feature—you would have to manually read all the log messages. Reverting a whole feature (i.e. a group of commits), is a true headache in the latter situation, whereas it is easily done if the --no-ff flag was used.
Yes, it will create a few more (empty) commit objects, but the gain is much bigger than the cost.
Examples :
git merge --no-ff    ===>>>>>
// => commit created at merge with proper message

Git merge ========>>>>>>
// --ff is by default, message/commit  will be ignored





This scenario is useful when revert task comes……



When to use webhooks 

From <https://dzone.com/articles/adding-a-github-webhook-in-your-jenkins-pipeline> 
Use webhooks to integrate applications with Bitbucket Cloud, for example:
• Every time a user pushes commits in a repository, you may want to notify your CI server to start a build.
• Every time a user pushes commits or creates a pull request, you may want to display a notification in your application.


have you ever tried adding GitHub webhook in Jenkins? In this blog, I will be demonstrating the easiest way to add a webhook in your pipeline.
First, what is a webhook? The concept of a webhook is simple. A webhook is an HTTP callback, an HTTP POST that occurs when something happens through a simple event-notification via HTTP POST.
GitHub webhooks in Jenkins are used to trigger the build whenever a developer commits something to the master branch.
Let’s see how to add build a webhook in GitHub and then add this webhook in Jenkins.
	1. Go to your project repository.
	2. Go to "settings" in the right corner.
	3. Click on "webhooks."
	4. Click "Add webhooks."
	5. Write the Payload URL as
https://228b9f82.ngrok.io/github-webhook/
Here, Payload URL is the URL where our Jenkins is running add github-webhook to tell GitHub that it is a webhook.
	• Content type: What kind of data we want in our webhook. I have selected JSON data.
	• Secret: Used to secure our webhook we can provide a secret in our webhook and ensure that only applications having this webhooks can use it.
	• SSL verification: This SSL Checker will help you diagnose problems with your SSL certificate installation. You can verify the SSL certificate on your web server to make sure it is correctly installed, valid, trusted and doesn’t give any errors to any of your users.
Which events would you like to trigger this webhook?
	1. Just the push event: Only send data when someone pushed into my repository.
	2. Send me everything: If there is any pull or push event in our repository we will get notified.
	3. Let me select individual events: We can configure for what events we want our data.
Click Create and a webhook will be created.

Here https://228b9f82.ngrok.io/ is the port or IP where my Jenkins is running.
Here is a problem you have to take care of if you are running Jenkins on localhost then writing https://localhost:8080/github-webhook/ will not work because Webhooks can only work when they are exposed to the internet.
So if you want to make your  localhost:8080 expose to the internet then we can use tool
Write GitHub-webhook to the ngrok tool refer to this link.
Now let’s see how to use this webhook in Jenkins.
	1. Go to Manage Jenkins -> Configure System
	2. Scroll down and you will find the GitHub Pull Requests checkbox. In the Published Jenkins URL, add the repository link
	3. Click on "Save."



Now go to the Jenkins pipeline and select "GitHub hook trigger for GITScm polling."
In this way, we can add a webhook to our job and ensure that everytime a developer commits a code to GitHub, our build will be triggered.



















*