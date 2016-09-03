---
layout: post
title:  "Sinatra Project"
date:   2016-09-03 19:09:16 +0000
---


Building the Sinatra project-WOT tracker.

As an online gamer, my favorite online game is World of Tanks. That was of course before starting LEARN.  It’s a game where a player can buy different WWII tanks from different nations  of different types and levels. The purpose of my app is to help a user track down all the tanks he/she has acquired. At first I thought it was a very simple flow and designing the tables and building the models wouldn’t take long. This is where I was wrong. And that’s my first piece of advice. Take time to design your tables. Use online table diagramming sites. It is much faster to design and faster to make any changes you wish. Your app starts from there.

After creating the tables and models it was time to build Content Management System. There are two approaches: The first one is from the outside in build each CRUD method rendering to the relevant erb file and the second way is from the inside out, to build all your models and tables and then link them to each CRUd step. Although I started creating the app using the second method I ended up following the first. And the reason is it is much easier when you have the interface ready and know where everything is. One other thing i did just for fun and to test it and see how it works, was two create two levels of security when filling in information in the forms section. One level in the controller with the flash[:message], and one in html by adding "required" attribute.  

This app definitely could have been much better. With more information to the user such as date acquired, type, tier etc.. But the purpose of this project is to understand making a CMS, knowing how to create it and build something on your own without the safety net of pre-written spec files.

