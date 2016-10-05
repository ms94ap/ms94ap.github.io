---
layout: post
title:  "Rails JS assessment"
date:   2016-10-05 14:43:45 -0400
---

Back to rails project and this time to complete the JS part. 

Confused as to where to start, I decided to work on the user. In order to improve user experience I added a jQuery to posts/index and posts/show. More specifically the producer/user can see all the posts in the app without clicking on individual post.I added a Next post link to render the post and when the user sees all the posts, the "Next post" link disappears. 

```
$(function () {
  $(".js-next").on("click", function(e) {
    e.preventDefault();
    var nextId = parseInt($(".js-next").attr("data-id"));
    var userId = parseInt($(".js-next").attr("data-user-id"));
      //  change routes to show all posts
    $.get("/users/" + userId + "/posts.json", function(data) { //data returns a list of objects
      // find next post
      var nextPost = data.find(function(post) {
        return post.id == nextId; //returns true || false
      });
      //  Update post information on page
      $(".userName").text(nextPost["user"]["name"]); // link each element to each  post with nextPost
      $(".postTitle").text(nextPost["title"]);
      $(".postBody").text(nextPost["description"]);
      $(".productName").text(nextPost["product"]["name"]);
      $(".productPrice").text(nextPost["product"]["price"]);
      $(".productMinimumQuantity").text(nextPost["product"]["minimum_quantity"])
      
      
      //add next link to each post - Todo
      // 1.create a var addNext where post.id is higher than current post.id
      var addNext = data.find(function(post) {
        return post.id > nextId;
      });
      
      if (addNext){ // 2. and if addNext is true then add Next
        $(".js-next").attr("data-id", addNext.id);
      } else {
        $(".js-next").hide(); // else hide Next.
      }
    });
  });
```

If a user has many posts I thought it would be really convenient for the producer/user to just have a list of all posts and be able to see only the description of each post rather than visiting each post individually. 

```
$(function() {
  $(".js-more").on("click", function() {
    var id = $(this).data("id");
    var userId = parseInt($(".js-next").attr("data-user-id"));

   $.get("/users/" + userId + "/posts/" + id + ".json", function(data){
    $("#" + id + ".postBody").text(data["description"]);
    
    });
  });
});
</script>
```

Finally another feature i added was to admin to be able to create a category without refreshing the page.

```
$(function () {

    function Category (name, products) {
      this.name = name;
      this.products = products; 
      this.successMessage = function() {
        return "Category " + this.name + " successfully created."
      }
    }
    $('form').submit(function(event) {
      
      event.preventDefault();
 
      var values = $(this).serialize();
 
      var posting = $.post('/admin/categories', values);
 
      posting.done(function(response) {
        var newCategory = new Category(response["name"], response["products"]);
        $(".resultMessage").text(newCategory.successMessage());
       });
    });
  });
</script>
```

Overall I would say that thanks to this project I finally understood many of the JS concepts and for the future i decided to add more features in the app such as for all users to render all the post.details at welcome.html.erb. 






