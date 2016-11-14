---
layout: post
title:  "Factories vs Services"
date:   2016-11-14 10:49:45 -0400
---

So what is the difference between Factories and Services? Very confusing at the beggining but reading this article below made it clearer and easy to understand.
From Todd Motto's web site:
https://toddmotto.com/factory-versus-service

Service

So what is Service?

A Service is just a function for the business layer of the application, it’s just a simple function. It acts as a constructor function and is invoked once at runtime with new, much like you would with plain JavaScript (Angular is just calling a new instance under the hood for us).

Think about it being just a constructor method, you can add public methods to it and that’s pretty much it. It’s a simple API, don’t overthink it.

When should you use it?

Use a .service() when you want to just create things that act as public APIs, such as the getEmails method we defined above. Use it for things you would use a constructor for. Unfortunately if you don’t like using constructors in JavaScript, there isn’t much flexibility if you want to just use a simple API pattern. However, you can achieve identical results by using the .factory() method, but the .factory() method is much different, let’s take a look.

Factory

Next, the confusing .factory() method. A factory is not just “another way” for doing services, anyone that tells you that is wrong. It can however, give you the same capabilities of a .service(), but is much more powerful and flexible.

A factory is not just a “way” of returning something, a factory is in fact a design pattern. Factories create Objects, that’s it. Now ask yourself: what type of Object do I want? With .factory(), we can create various Objects, such as new Class instances (with .prototype or ES2015 Classes), return Object literals, return functions and closures, or even just return a simply String. You can create whatever you like, that’s the rule.

Conclusion

Both .service() and .factory() are both singletons as you’ll only get one instance of each Service regardless of what API created it.

Remember that .service() is just a Constructor, it’s called with new, whereas .factory() is just a function that returns a value.

Using .factory() gives us much more power and flexibility, whereas a .service() is essentially the “end result” of a .factory() call. The .service() gives us the returned value by calling new on the function, which can be limiting, whereas a .factory() is one-step before this compile process as we get to choose which pattern to implement and return.