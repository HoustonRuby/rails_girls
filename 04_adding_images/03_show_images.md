#Uploading and Viewing Chirp Pics

We'll need to add an upload field to our chirp form so that. First let's add it to our form. Open up `app/views/chirps/_form.html.erb` and add:

```rails
<%= form.file_field :pic %>
```
after the message field.

##Permitting Pic in the Chirp `Controller`

We'll need to tell Rails that we allow editing of the newly added pic property. Lets open `FILE PATH` and add `:pic` to:

```rails
def chirp_params
  params.require(:chirp).permit(:author, :message, :pic)
end
```

##Viewing Our Pics

We'll also need to add the images to our index and show pages. We'll do this by adding:

```rails
<%= image_tag @chirp.pic.url %>
```
to both `FILE PATH` and `FILE PATH`
