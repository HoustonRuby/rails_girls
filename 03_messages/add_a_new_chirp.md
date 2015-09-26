<!-- TODO: need to link adding chirps page on the list page somewhere in this section -->

# Add a new chirp


| URI Pattern | Controller #Action | What-should-it-do? | Example action code |
| -- | -- | -- | -- |
| /chirps/new | **chirps#new** | Show a form on a page for someone to fill out a new chirp | `Chirp.new` |
| /chirps | chirps#create | Create a new chirp that get's saved | `Chirp.create(body: 'a body', author: 'some author')` |

We'll start by making a form on  [http://localhost:3000/chirps/new](http://localhost:3000/chirps/new).  In the `new` action/function in  `app/controllers/chirps_controller.rb`, we will add:

```rb
    @chirp = Chirp.new
```
![](../images/sublime_new_chirp_controller.png)

And in `app/views/chirps/new.html.erb`, let's make a form:

```html
<h1>Make a Chirp</h1>

<%= form_for @chirp do |f| %>

  <div>
    <%= f.label :author %>
    <%= f.text_field :author %>
  </div>

  <div>
    <%= f.label :body %>
    <%= f.text_area :body %>
  </div>

  <div>
    <%= f.submit 'Chirp!' %>
  </div>

<% end %>
```

Now, if we go to [http://localhost:3000/chirps/new](http://localhost:3000/chirps/new), we'll see a form for making a new chirp.

![](../images/chrome_new_chirp_form.png)

Let's try to chirp by filling out the form and pressing "Chirp!"

![](../images/chrome_form_chirp.png)

![](../images/chrome_chirp_error.png)

> What happened?  Discuss with the coach and look at the code the `form_for` function made for us in our HTML using Inspect Element.

Since submitting the form goes to the **chirps#create** controller action, **chirps#create** should take the parameters from the form and make a new Chirp with that.

Let's add the following to our `app/controllers/chirps_controller.rb`:

```rb
  def create
    @chirp = Chirp.new(params[:chirp].permit(:author, :body))
    if @chirp.save
      redirect_to chirp_path(@chirp)
    else
      render 'new'
    end
  end
```
Our controller should now look like this:

<!-- TODO: update this create to include the else. -->
![](../images/sublime_controller_create.png)

Now, when we submit...

![](../images/chrome_made_new.png)

we get redirected to the new chirp.

> Review with your coach.  What does the `.permit` in our code help do? What did we work with?

For convenience, let's add a link to adding a new chirp on [http://localhost:3000/chirps](http://localhost:3000/chirps).

We can do this by adding to `app/views/chirps/index.html.erb`, just below the heading:

```rb
<%= link_to "Make a new chirp", new_chirp_path %>
<hr>
```
![](../images/sublime_all_with_new.png)

[http://localhost:3000/chirps](http://localhost:3000/chirps) will now have a link to make new chirps.

![](../images/chrome_all_with_new.png)
