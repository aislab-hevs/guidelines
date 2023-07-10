# AISLab Guidelines

## 📝 1. Documentation

### 1.1 The Bare Minimum 

Every project should contain at bare minimum a README file in the root directory. Normally this is written in markdown, but feel free to use whatever you like. This file should contain a short description of the project and all technical instructions for the following :

1. How to set-up the project for local development
2. How to deploy the project
3. How to maintain the project

Any other documentation should be in a dedicated folder called something like "documentation" or "docs". It is nice to push documentation to GitHub (unless it is too large) - this way everything is in one place, and you will never find code that has no context.

ℹ️ The goal of this README is that any developer can pull the code, run the project locally and deploy the project without needing any extra information. The simplest way to check if this is the case, is to ask someone to run the project locally without any help or prior experience with the project. You can use their feedback to improve the README!

### 1.2 A User Guide

Every project is only as good as it's documentation. The best developer in the world can make a bad application, if no one understands how it works.

A User Guide can help the users of an application, by showing them the intended utilization, how features work etc. However, it can also be useful for developers! Consider the following points : 

* A new developer can see how the application was designed
* A new developer can see how certain features are supposed to work, without reading the code
* A new developer can see when a feature will change dramatically, without needing to check the code

A User Guide does not even need to be complicated, the most basic version can just be a screenshot of each page/screen, with a few bullet points to explain how it works. 

In summary :

1. Your stakeholders will send less emails
2. Your developers won't ask as many questions
3. You can give it to people instead of organizing a meeting


### 🌐 1.3 Environment Variables

Projects should use a .env file to store any variables that are specific to the deployment, there are other ways of doing this but .envs are the most universal. If you use another type of file or technique, make sure it is documented in the same way.

Standard practice is to create two files : 

 * A .env that is .gitignored, this way we won't accidentally push sensitive data to the internet
 * A .env.example file that contains a list of all the used variables with dummy values, or the local development variables

 I like to document this using markdown tables in the project README, which looks like this :

| Configuration Variables | Description                                         |
|-------------------------|-----------------------------------------------------|
| DEV_MODE                | Set to "True" when developing locally               |
| DATABASE_USER           | The user  created to access the database            |
| DATABASE_PASS           | The password for the default access user            |
| DATABASE_ROOT_PASS      | The password for root user (required)               |

I like to separate the variables into two categories : configuration and deployment. You can add comments in a .env file to indicate extra information like this and make seperate markdown tables to separate any categories, like so :

| Deployment Variables | Description                                            |
|----------------------|--------------------------------------------------------|
| TRAEFIK_BACKEND      | The name of the backend in Traefik                     |
| TRAEFIK_URL          | The URL that the app will be served on                 |
| TRAEFIK_NETWORK      | The name of the network in Traefik                     |

And an example of a .env.example :

```
# api config
DEV_MODE=True
SECRET_KEY=this_is_an_example

# database config
DATABASE_USER=dev
DATABASE_PASS=dev
DATABASE_ROOT_PASS=example_password

# traefik configuration
TRAEFIK_BACKEND=traefik_network
TRAEFIK_URL=my.app.hevs.ch
TRAEFIK_NETWORK=dev
```

⚠️ It is very important that these are documented, these variables are normally absolutely crutial to running and deploying the project. You don't want to have to organise a meeting just for someone to say "Oh, you forgot to add the VERY_IMPORTANT_VARIABLE in the .env, it won't work without it. Have a nice day!".

## 💾 2. GitHub

GitHub is great, try and use it's features! It would be nice if we had access to GitHub Pro but it still has many, many great features that not everybody uses.

### 🐞 2.1 Bug Reporting

GitHub repositories have an "Issues" tab by default - try using it, it's pretty great! You can create tags to help organise any bugs, crashes or issues found in the product, and it is very accessible even to people that aren't developers!

It works similarly to many other reporting systems you can assign people to bugs and update their statuses - this let's you track the lifecycle of a problem from its discovery to its (hopeful) death.

Try and remember the best-practises for reporting bugs - you can even add a section on your README if you want about how to report problems in your application. Include at bare minimum the following pieces of information :

1. **The expected behavior** (what should happen)
2. **The observed behavior** (what actually happens)
3. **Steps to reproduce the problem** (how you made it happen)
4. **What environment did the problem occur in** (what version, browser, OS etc.)

### 🌳 2.2 Branches

When you start working on a new feature, bug fix or something else, create a new branch! When there are multiple people working on the project at the same time this is absolutely imperative, please get into the habit of doing it, even if you are working alone! We do this to keep our changes organised, separated and understandable.

It is nice to have a naming convention for your projects branches, but by default you can use this simple one :

```type/name-of-branch```

For the ```type/``` you can put what the work you are doing actually is. For example you could use one of the following :

* ```feat/``` for a new feature
* ```fix/``` for fixing a problem
* ```docs/``` for updating documentation
* ```test/``` for testing something
* ```deploy/``` for a specific deployment

The ```name-of-branch``` should be short, describe what you are doing and be understandable for any developer of the project. You should **ONLY** use dashes for spaces and only non-capital letters - remember your branch name will be part of a URL in some form or another.

Make sure that if you want to use your own naming convention / branching strategy that you write it down in your README - remeber that the goal of the README is to contain **ALL** the informaton needed to start developing!

Once you have finished working on your branch you can then do one of two things, depending on how the project is being run :

1. **You are a solo developer** - you can checkout main and run ```git merge my-new-branch```
2. **You are working in a team** - you can create a Pull Request

⚠️ Sometimes it is OK to make small commits to the main branch to quickly change things. However, if you see anyone making large changes to the main branch of a project then please ask them to stop. Committing directly to main works just fine, until it doesn't. If you make a mistake on the main branch and break the application it can be very difficult to detect, fix and repair unless you are very experienced with the git CLI.

### 🔎 2.3 Pull Requests

Anytime you are working on a project with more than one developer it is **ESSENTIAL** that you use Pull Requests. The idea is that, once you have finished your work, another developer looks at what you have done, reviews it, and then lets you merge your changes. This is advantageous for many reasons :

* All developers know what changes have been made
* All the code is checked to be understandable, clean and clear
* You will find problems that you missed by yourself
* Both developers learn more about the project / technologies
* The project is no longer a big secret that only one person understands

ℹ️ If you ever work in a large development company being able to manage work into Pull Requests is mandatory. If you want to work on large applications that run at scale then working in this manner is essential. It is not only beneficial to the team and product, but this skill can help you become a more senior member of a dev team - where you are able to over-see and manage the work of others!

## 🙏 3. On-boarding

On-boaring is the process of taking a new developer and getting them to a point where they can work on a project independantly without the need for supervision. You can imagine it like hiring a new sailor for your boat - would you let someone on board your ship if they didn't know how to rig the sails⛵?

Every project is different and every developer has different skills/experiences so it is up to you to manage this in the best way possible, but here are a few basic steps that I have found useful in the past :

1. Ask the developer to read the **offical documentation** of any languages or frameworks that the project uses
2. Ask the developer to read the **ENTIRE** project documentation and write down any questions they have
3. Ask the developer to then read over the code of the **ENTIRE** project and write down a list of questions
4. Add the relevant answers to these questions to the **project documentation**
5. Ask the developer questions about the complex features of the project, and explain how they work
6. Explain the branching strategy, commit etiquette, Pull Request system, bug reporting system etc. to the developer
7. Create a few fake changes to make to the code - this can be things like adding new routes to APIs, changing the UI, adding multi-language text, adding unit tests etc.
8. Get the developer to make a new branch, make their changes in commits, create a Pull Request and wait for a Review
9. Review their changes and ask for some modifications to be made, when you are satisfied you can delete the branch
10. Now the developer should know exactly what to do from start to finish if they are given a development task on the project!

If you do something similar you should get a lot of feedback on how easy the project is for a new developer to pick it up and start working. Try as much as possible to let your documentation do most of the work, adding to it every time a question is asked or something is not understood. The end goal is to have documentation that is so good that any developer can start without your help.

If you have to spend a lot of time with a developer to help them get started or fix something it is normally **YOUR** fault - or more accurately your documentation is **BAD**!

## 💀 4. Off-boarding

So if on-boarding is when a new developer arrives, off-boarding is when an old developer leaves. The goal of off-boaridng is to make sure the project will have the same quality in the future as it has had in the past. Usually if you need to spend a lot of time off-boarding it means that you did not spend enough time on-boarding, or you were a solo developer on the project (which we are trying to avoid).

The best way to off-board is simply to not have to. If every project has at least two developers that are capable of "owning" the project (they know the project, code and technologies) then it should mean that **someone leaving should never matter!**

Of course in reality there are always details that one developer has that no-one else knows - hopefully you are starting to see that this could have been avoided in the first place by writing and updating your documentation. Remember in the on-boarding section where you **updated the documentation every time your new developer had a question**? Good job, it turns out that just **saved you from ever having to off-board**!

### 🆘 4.1 Reality

In reality things rarely go perfectly, so here are some steps you can take to off-board successfully if you or another "project owner" are about to leave :

1. Make sure you have at least one other developer
2. Ask them to read through the offical documentation for the technologies, the documentation for the project and even this document!
3. Like before, get them to write down any questions that they have
4. Sit-down with your new developers, go through the questions and **update your documentation**!
5. You can even repeat the process of creating some fake tasks, getting them to send a Pull Request and reviewing it, like for the on-boarding (depends on the experience and ability of your developers)


## 🧑🏿‍🤝‍🧑🏻 5. People

People are important, they basically made everything.

### 5.1 Specialists

We have a wide range of skills and specializations here at AISLab, we need to use this to our advantage, but in an efficient way.

We should create a list of core skills that exist in AISLab - who has them, who you can ask about them, who introduces which technologies.

For example :


| Front-end Specializations | Humans                                                 |
|---------------------------|--------------------------------------------------------|
| Flutter                   | Ben, Yvan                                              |
| React                     | Ben, Yvan, Ekaterina                                   |
| Web (HTML, CSS)           | Ben                                                    |

| Back-end Specializations  | Humans                                                 |
|---------------------------|--------------------------------------------------------|
| Python                    | Yvan, Ben                                              |
| Java                      | Yvan, Ben                                              |
| PHP                       | Ben                                                    |
| NodeJS                    | Ben                                                    |
  
| Machine Learning          | Humans                                                 |
|---------------------------|--------------------------------------------------------|
| Supervised Learning       | Victor, Yvan                                           |
| Unsupervised Learning     | Victor, Yvan                                           |
| Explainable Layers        | Victor                                                 |
| Data Analysis             | Victor, Yvan                                           |

| Project Management        | Humans                                                 |
|---------------------------|--------------------------------------------------------|
| SCRUM                     | Ben, Yvan                                              |

We can assign one of these specialists to meet with any new employees or students, introduce them to how we use the technology, our best practices etc.

One role that we should assign, is the role of SCRUM Master. This can either be on a per-project basis, or a SCRUM Master for the whole company. Normally this is a full-time job, but we can **at least** have someone dedicate some time to each project every week to make sure SCRUM is being adhered to. 
	
### 5.2 Second-in-command

Every project requires that there is a second developer that knows the project very well. In the worst case, such as an accident or illness, there needs to be someone that can pick up the project almost instantly, that can at least perform basic deployment/maintainance/updates to the code.

This is **mandatory**, not only for unforseen consequences - but also for vacations, job changes and normal day-to-day activities. 

Imagine that your computer explodes and you lose your private keys. Now you cannot access the server and you cannot access the GitHub CLI.

## 👨‍💻 6. Working Efficiently

### 6.1 Don't build something twice

Something that we have seen quite often are two people, using the same technology, developing something very similar. It is very rare that you will ever start a project that has absolutely no relation to development that has already been done.

Before you start developing a project, check our resources :

* **Who** is the specialist of the technology we are using?
* **What** projects exist within AISLab that are similar to this one?
* **What** Open Source projects exist that are similar to this one?
* **How** did we solve this problem before?
* **Who** solved this problem before?

It is **very likely** that if you ask yourself good questions like this, you can already reduce your development time massively.

It is **very likely** that the last AISLab developer using technology X also had to solve the same problems you are facing, read their code, or ask them!

Similarly, if you developed something, and you see someone is working on something similar - **show them your project**!
	
### 6.2 Your time is important
In our increasingly connected world, finding the mental space for focused, uninterrupted work can be challenging.

- Research by the Univesity of California shows the average office worker is interrupted roughly every 4-6 minutes
- A study by Microsoft revealed that the average human attention span has declined by 33% since the year 2000
- A study from the University of London showed that people's IQ decreased by 10-15 points when distracted

Developing software is not easy. It requires long periods of intense concentration, complicated data structures and a lot of testing.

Working at the Swiss Digital Center is amazing, but there is always something happening. You will most likely find yourself being invited to 10 seminars every week, at least one meeting for every project, people asking you for help or your opinion on something etc. etc.

A method that can help with this is to start blocking off your development time in your professional calendar. This way : 
* Everyone can see that you are busy
* You have a flexible schedule - you have the **choice** to say yes or no to someone

A few tips:

- Schedule dedicated blocks of time for deep work and protect these periods from interruptions
- Remove all possible distractions before you start working (phone out of sight, turn notifications off, close email & messaging tabs)
- Work on one task at a time instead of trying to multi-task


**Do not be afraid to say that you are busy!** 

People will understand, you need uninterrupted time to develop your project, it is as simple as that.
