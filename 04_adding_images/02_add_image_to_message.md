#Add Pic to Chirp Model

Now we need to let rails know our chirps are going to have images. Lets open the chirp model at `app/model/chirp.rb` and add the pic property:

```rails
has_attached_file :pic, default_url: "/images/:style/missing.png"
```
right after the first line.

##Telling Rails about our Chirp Pic

Now that we've added the property to our `model`, we'll need to build a migration to describing our new property to `ActiveRecord`. Lucky for us, the developers of Paperclip realized that every developer would need to take this step so all we need to do is type in the command line:

```bash
$ rails generate paperclip chirp pic
```

We'll then see:

<!-- Insert Image of create message in bash -->

If we refresh our browser, we'll see:

![](../images/chrome_error_rake_db.png)

We've seen this before! In Chapter 4 we fixed this by typing:

```bash
$ rake db:migrate
```

in our command line to migrate new data into our chirp model. If we do this again and refresh our browser, we'll see our Chirp page!

