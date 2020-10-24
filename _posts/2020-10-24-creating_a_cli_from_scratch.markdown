---
layout: post
title:      "Creating a CLI from scratch"
date:       2020-10-24 21:03:08 +0000
permalink:  creating_a_cli_from_scratch
---

## How to start?
When starting this final project for our module it seemed overwhelming: 
1. What is an API and how am I going to create objects from its information? 
2. What is a repository? 
3. How do I set up my project? 
4. What IDE should I use?
4. How do I connect my project to github? 
5. How do I clone a project?

## Learning experience
Yes, we were told to start with the API. I decided to set up a project before I picked an API because I didn’t want to have nothing to show for my time, it was taking me forever to pick an API. I now realize that once I picked my API I should have started the project setup over, copy and paste to get the proper naming. I thought the name could be easily changed after setup...poor assumption. Since I worked in google_cli repository all of my `git commit -m “messages” `would be lost and we are needing those requirements for the evaluation of my CLI.  

## When it starts to click
Once I got my `ruby ruby bin/run`  to connect to CLI, which connected my API it took me a while to create the objects because I had forgotten that I tampered with my `environment.rb`. Since there is no spec file for the first time it made me get a lot more comfortable using the `binding.pry` to see exactly what is happening with my code and when. I also found myself using this tool to test the code that needs to be written much more, which allowed me to find solutions faster. Me “Why would Brewery.new not work?” My API was not able to communicate with my Brewery class until my environment file included `require_relative “./lib/brewery.rb”` which connects the Brewery class with the rest of files. Once everything was communicating properly and I had my objects the build became much easier/familiar.

## Wrap up
Now it’s time for the assessment. Time to find out if I actually know what I’m doing, can communicate my code properly, and possibly expand functionality. 

