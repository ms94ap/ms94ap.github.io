---
layout: post
title:  "Rails Project"
date:   2016-09-09 15:25:27 +0000
---

My rails project is a wholesale food and beverage e-store where producers as well as wholesalers can advertise their products.

The welcome page shows all posts created and a visitor can see at any time the posts. But to see additional information such contact information of the producer, has to either log in or sign up.  

For the application to run properly I had to create different roles. An admin and a user.  The role of admin is to create new categories(sub-categories to be added soon) for the users to pick from when posting their products, delete or block a user (to be added soon) etc. So I build admin/category_controller.rb but the challenge I faced here was to add category to posts. And that was my first mistake. The solution was quiet simple although it took me some time to figure it out. I shouldn't add category to posts but category to products. 

```
def product_attributes=(pro_attributes)
  
    product = Product.create(name: pro_attributes["name"], 
    	minimum_quantity: pro_attributes["minimum_quantity"], 
    	price: pro_attributes["price"])
    product.categories << Category.find(pro_attributes["category"])

    self.product = product
		end
```

The next step was to change the associations in models/product.rb...again.

```
class Product < ApplicationRecord
  belongs_to :user
  has_many :product_categories
  has_many :categories, through: :product_categories

```

and define category_name:

```
 def category_name=(name)
    self.category = Category.find_or_create_by(name: name)
  end
```
	
	Next and final step was to add in product controller:
	
	`def create
     category = Category.find_or_create_by(name: params[:category_name])
     Product.create(product_params, category: category)
   else
     render :new
   end
 end

 private
 
 def product_params
   params.require(:product).permit(:category, :name, :minimum_quantity, :price)
 end
end`
	
	

But the most challenging part was creating tables and migrations. I had to change them several times. Designing associations before you start building your application is a good way to start but there is no guarantee it will be correct, as logic of the application keeps changing when you start breaking down each part of it piece by piece. 

Overall it was fun building this app and it can be really frustrating, especially when using Devise, but I learned a great deal during the process and I can now appreciate even more Sinatra's value in learning Rails!!!
