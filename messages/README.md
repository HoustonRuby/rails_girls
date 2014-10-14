# What is a message or a Chirp?

> Let's discuss!
>
> For example, a message should have an author, a chirp body...what are some other things?


## Let's tell Rails our definition of messages!

Let's command Rails to work with these kinds of messages:

```bash
$ rails generate model Chirp body:text author:string
```

Since we are writting Chirper, let's call these messages chirps!

Rails will now make something called a "`model`" to represent this idea of a Chirp.  With a "`model`", Rails can associate different actions to do with Chirps, and can save different Chirps we'll be making to a *database*.

> Discuss more with your coach about what a "`model`" is and what a *database* does.

Our commandline should now look like this:

![](../images/terminal_model_messages.png)

Just like before when we did `rails generate controller ...`, Rails has made some new files for us.

Let's refresh our page and see if anything changed.

![](../images/chrome_error_rake_db.png)

Ouch, an error!  But once again, Rails guides us by telling us what to do to fix the problem.  Here, I've highlighted the important part we should run in our commandline:

```bash
$ rake db:migrate
```

What we are doing is telling `rake` to "migrate" the new information we've made about how Chirps are structured into the database.

Now, we should see this in our terminal:

![](../images/terminal_rake_db_messages.png)

The really cool thing is that something called *Active Record* made a table for us called "chirps" and it reports back to us in the terminal saying,  `create_table(:chirps)`.

<!--I just made this up so I actually need to research this a little more-->
> *ActiveRecord* is a really neat thing that actively keeps a record of all the changes our database is going through.  In case something goes wrong, or you are trying to share the same database structure and information with someone, *ActiveRecord* will be able to "migrate" you whatever state it has a record of.
>
> Discuss more in depth with your coach what *ActiveRecord* and `rake` are.

Now, if we reload our page in Chrome, we should see our expected index page again.

It works again, but it doesn't seem like anything has changed.  That is fine.  We need to be able to perform some actions on Chirps first.

# What should we be able to do with a Chirp?

> Let's discuss!  For example, we need to be able to make new ones.

## Let's try doing some of these things!

As we discussed, we should be able to **create** a new Chirp, **show** a Chirp, **update** a Chirp, **delete** a Chirp, and **list** all our Chirps.  Rails has a way for us to do these things in the commandline.  It's called the `rails console`.   Let's go to the commandline and try:

```bash
$ rails console
```

> Ask your coach what is the Rails console.

We should see:

![](../images/terminal_rails_console.png)

The `>` means that the Rails console is waiting for us to tell it things to do.

Let's try a couple things:

```rb
> Chirp.new
```

Take note of the highlighted line:

![](../images/terminal_rails_console_chirp_new.png)

Here, we can see the `body` and `author` properties that we told Rails about earlier, along with an `id`, a `created_at`, and a `updated_at`.  These will come in very handy later on.

Next, let's making a new Chirp that has a `body` and an `author`.

```rb
> first_chirp = Chirp.new(body: 'the first chirp', author: 'Big Bird')
> first_chirp.save
```

This will make a new chirp and also save it to the database.  The `Rails console` nicely tells us that a transaction with the database has happened.

![](../images/terminal_rails_console_newsave.png)

Let's try the following:

```rb
> first_chirp.body
> first_chirp.create_at
> first_chirp.id
```

Each of these let us look at what's at each attribute.

With the id, we can look at the chirp with:

```rb
> Chirp.find(1)
```

We can update the `body` with:

```rb
> first_chirp.find(id).update(body: 'The first chirp, with an edit!')
```

Let's look at all the chirps we have in our table:

```rb
> Chirp.all
```

The commandline shows us the updated chirp!

![](../images/terminal_chirp_all.png)


Let's make some more chirps using a shortcut function that will make a new chirp and save it at once:

```rb
> Chirp.create(body: 'Worm', author: 'The Early Bird')
> Chirp.create(body: 'Hello!', author: 'Big Bird')
> Chirp.create(body: 'I am yellow', author: 'Big Bird')
> Chirp.create(body: 'And it was all yellow', author: 'Coldplay')
> Chirp.create(body: 'bird, bird, bird', author: 'Word')
```

Looking at all chirps using `Chirp.all` again, we can see that there are many more chirps!

Some other things to try:

```rb
> Chirp.find(2)
```

```rb
> Chirp.find(1).destroy
> Chirp.all
```

```rb
> Chirp.where(author: 'Big Bird')
```
<!-- TODO: add link to things to try-->

> Talk through these different things with your coach.  See what else you can try here:
>
> What could we do?

## Let's add pages for the things that we can do.

Doing these things on the commandline is super fun and all, but if we want users to be able to do what we did with Chirps, we will need to map these capabilities to some pages.

The ability to:
* create a new thing,
* list all of those things,
* show a specific thing,
* update a specific thing, and
* delete a thing

are very common and Rails has a way for us to start setting these up quickly.

We can start by adding routes in the `config/routes.rb`.  In that file, let's add that in a new line right after `do`:

```rb
resources :chirps
```

`config/routes.rb` should now look something like this:

![](../images/sublime_routes_chirps_resource.png)

This is a shortcut to make routes for doing things with a '`resource`' really quickly.

If we reload our page, we see that it's still running.  So what has this `resources` thing done for us?  We can find out by going back to the commandline and asking Rails:

```bash
$ rake routes
```

We should see:

![](../images/terminal_resources_routes.png)

> Let's talk about what routes are and what this idea of a resource is.

## Linking the actions to the pages

Let's see what happens when we try to go to one of these routes, namely [/chirps/new](http://localhost:3000/chirps/new).

![](../images/chrome_try_chirps_new.png)

We can tell Rails to make a controller like we did before.

```bash
$ rails generate controller chirps
```



<!---->









We can line up what we saw from `rake routes` for chirps with what we did in the console like so:

| Prefix | Verb | URI Pattern | Controller#Action | Example action code |
| -- | -- | -- | -- | -- |
| chirps | GET | /chirps(.:format) | chirps#index | `Chirp.all` |
|  | POST | /chirps(.:format) | chirps#create | `Chirp.create(body: 'a body', author: 'some author')` |
| new_chirp | GET | /chirps/new(.:format) | chirps#new | `Chirp.new` |
| edit_chirp | GET | /chirps/:id/edit(.:format) | chirps#edit | `Chirp.find(id)` |
| chirp | GET | /chirps/:id(.:format) | chirps#show | `Chirp.find(id)` |
|  | PATCH | /chirps/:id(.:format) | chirps#update | `Chirp.find(id).update(body: 'a body')` |
|  | PUT | /chirps/:id(.:format) | chirps#update | `Chirp.find(id).update(body: 'a body')` |
|  | DELETE | /chirps/:id(.:format) | chirps#destroy | `Chirp.find(id).destroy` |


