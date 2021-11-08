# Jenkins

Jenkins is the CI/CD software tool that we as a team might decide to use for our project. The objective is to build a pipeline to automate the process of testing, building and running our project. 



## What is CI/CD?

CI/D stand for continuous integration and continuous delivery. The meaning of these terms is:

* Continuous integration: the process of constantly reviewing and testing the code and generating documentation. 

* Continuous delivery: scheduling the production of software in short cycles. The objective is to create software with short increments to avoid deliveries of big amounts of code that might be more susceptible to bugs and errors. 

## What is a pipeline?

In software development, a deployment pipeline is a system of automated processes designed to quickly and accurately move  new code additions and updates from version control to production.

In other simpler words, a tool that will help us automate the process of software development. 



## The tool 

### Advantages 

* Stable, no bugs 
* A lot of documentation on line
* Many plug ins at our disposal that might allow very diverse functionalities

### Disadvantages 

* Server-aimed: if we don't agree to hire external hosting, each one of us will have to install Jenkins in order to use its functionalities. 



### Set up Jenkins (linux)

* First, install Jenkins in your computer (distribution dependent)

* Enable and start the service: 

  `$systemctl enable jenkins`

  `$systemctl start jenkins`

* After that just access `http://localhost:8090`

  * Security can be disabled, here is how: https://mohitgoyal.co/2017/02/10/disable-security-in-jenkins/

* And now we are done setting up the tool



### Set up the pipeline

* First, we are going to need the github  plugin in jenkins, on the side bar: manage jenkins-> manage plugins and click on the available tab. Search for github, tick the box and click install and restart below. 

* Now that we have the plugin, we will have to create a project: 

  * New item-> freestyle project 
  * Tick github project: After that, a bar will appear in which we have to put the URL of the project that Jenkins will be listening to.
  * We have to change source code management to Git. After that, a bar will appear in which we have to put the URL of the repository that Jenkinswill be listening to. No credentials are needed if the repository is public, else we will have to create a new creedential token. 
  * **Careful**: branch specifier must be changed to "main"
  * In build triggers: GitHub hook trigger for GITScm polling
  * After that, in build, we will have to tell Jenkins what to do with the code with every push. [TODO]

* After we have our project, we will have to set up a webhook, which is a tool that will tell github who to warn every time a push is made. Unfortunately, given the nature of IP's, we will need an additional tool to continuously expose one of our ports, that tool will be **ngrok**

  *  After installing ngrok (fairly simple), we just have to type:
    * `ngrok httpd <port>` . Where <port> is the port that Jenkins is listening to (default 8090)
    * After that, we just have to copy the hexadecimal token in the  first line of "forwarding", it will have the format <http://{hex}.ngrok.io>.
  * Then, we go to the target repository-> settings-> webhooks and create a new one. In the payload URL we must input  http://{hex}.ngrok.io/github-webhook/

* If we have correctly performed the setup, everytime we push a change in the repository, a message should appear in the ngrok terminal with the message "OK 200" and Jenkins will take the code and perform the commands specified in "Build"

  