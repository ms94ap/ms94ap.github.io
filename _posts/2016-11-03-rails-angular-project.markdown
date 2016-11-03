---
layout: post
title:  "Rails Angular Project"
date:   2016-11-03 10:49:45 -0400
---

Welcome to Bedouin.
The term 'Bedu'in the Arabic language refers to one who lives out in the open, in the desert. Bedouins are generally open-minded and interested in what is going on in their close and far surroundings since this kind of knowledge has always been a vital tool of survival. Bedouin is an application in which the user can add stores, restaurants, favorite music etc. and in general places he visited.

There are two ways to build an app. Either start building the front end with AngularJs and then build your back end with Rails or the other way round. I prefer to start from bottom up. Setting up Rails didn't take took long.

Some key points of the project

1) Adding and removing gems
Working with turbolinks can be challenging. The link explains the differences between turbolinks and Angular JS and how you can set up your files.

[](http://stackoverflow.com/questions/14797935/using-angularjs-with-turbolinks)
But should you choose to delete it you should also remove it from asset pipeline.

In the gemfile I also included:

```
* gem 'pry'
* gem 'bower-rails'
* gem 'angular-rails-templates'
* gem 'active_model_serializers'
```
Bower is  package manager supplying a huge range of Javascript and CSS frameworks and plugins, which runs via Node. Below is the link on how to install it:
https://github.com/rharriso/bower-rails

2) Getting single store back from a list.

First thing is to set up the route in routes.js

```
.state('home.store', {
                    url:'stores/:id',
                    templateUrl:'stores/store.html',
                    controller:'StoreController as vm'
                })

```

In Stores.Controller.js I have created a callable method getStore with id as an argument which will return from StoreFactory the getStore method with the id.

```
function getStore(id){
			return StoreFactory.getStore(id);
```
In StoreFactory the getStore is returning a $http.get request of stores plus the storeId which was passed as an argument in the method

```
function getStore(storeId) {
	
			return $http.get('/stores/' + storeId)
				.then(handleResponse)
        				.catch(handleError);
```
I edited the activate method defined in the Stores.Controller.js

```
function activate(){
​// get a single store
			if ($stateParams.id) {
				getStore($stateParams.id)
					.then((data) => {
						return vm.store = data
					})
  			} else {
    			getStores();
	  		}
		}
```
and finally pass $stateParams as an argument in the StoresController function

3) Services vs factory.
At first those two were confusing but reading a couple of articles it is much clearer what both do. So all in all Factory returns objects and Services return functions. (More to come soon)

ToDo
1. I will continue the project by adding more categories.
2. I will reform the app to create users
3. Add bootstrap of course