## Permitting Pic in the Chirp `Controller`

We'll need to tell Rails that we allow editing of the newly added pic property. Lets open `app/controllers/chirps_controller.rb` and add `:pic` to:

```rails
def chirp_params
  params.require(:chirp).permit(:author, :message, :pic)
end
````

##New Chirps with Pics

Now that the controller has permission to change add a pic we'll need to add a way to upload a file. Let's open up `app/views/chirps/new.html.erb` and add:

```html
<div>
  <%= f.label :pic %>
  <%= f.file_field :pic %>
</div>
```
after the body field. Now when you go to add, you'll see:

<!--Insert image of new create page-->

Add the same code to `app/views/chirps/edit.html.erb` and you'll then seed:

<!--Insert image of new edit page-->

##Viewing Our Pics

After we've uploaded a new chirp with an image, we'll want to see it. First let's add:

```html
<p><%= image_tag @chirp.pic.url %></p>
```
to `app/views/chirps/show.html.erb`. Now when you upload a chirp, you'll see:

<!--Insert image of new show page-->

Repeat for `app/views/chirps/index.html.erb`, and you'll now see:

<!--Insert image of new index page-->
