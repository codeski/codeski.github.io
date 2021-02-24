---
layout: post
title:      "Rails: rendering partial collections replace iteration"
date:       2021-02-24 16:57:02 -0500
permalink:  rails_rendering_partial_collections_replace_iteration
---


To review, if we had this type of logic in our view 
view/posts/index.html.erb 
`
<% @posts.each do |post| %>
<h2><%= post.title %></h2>
<p><%= post.content %></p>
<% end %>
`
It would show us all the posts created. However, we don’t want this logic in our views. We also want to make our code more efficient and scalable. We want to create a partial for a post. 

view/posts/_post.html.erb
`
<h2><%= post.title %></h2>
<p><%= post.content %></p>
`
And now we modify our view/posts/index.html.erb to 
`
<%= render partial: ‘post’, collection: @posts %> 
Or (more abstractly)
<%= render @posts’ %> 
`
We can do this because we followed the implicit formatting that rails accepts. But what if we don’t follow Rails convention when naming our partial and we put it under a different folder in our views.

view/users/show.html.erb
`
<% @user.posts.each do |post| %>
<h2><%= post.title %></h2>
<p><%= post.content %></p>
<% end %>
`
view/posts/_different_naming.html.erb (not that we would ever call a partial this, but it helps to understand.)
`
<h2><%= different_naming.title %></h2>
<p><%= different_naming.content %></p>
`
*Notice that the partial variable needs to be called by the name given to the partial in order for it to work.* 

Now our iteration can be replaced in 
view/users/show.html.erb
`
<%= render partial: ‘posts/different_naming’, collection: @user.posts %>
`

