# Make authors into Users

Our Chirper app is looking pretty good right now, but we can up the ante a little bit and have users.  Each of our authors could be a user with a `username` and a `password` so that they can log in and chirp on their own!

We can get Rails to help use with this update!  We'll do this by:

1. Asking Rails to add a new "`model`" for Users.
  * Each user should have
    1. An `email` to sign in with
    1. Password information -- more on this later
    1. A `name` for displaying as author
  * Tell Rails what should happen when we create a user.
    * Whenever we create a new user, Rails should help us store our password secretly
1. "`Seed`" our app with a user per author.
1. Tell Rails that each Chirp "`belongs_to`" a user and that each user can "`has_many`" Chirps.
1. Update exisiting Chirps with the matching users by author name.
1. Remove `author` from the Chirps "`model`".
1. Update the pages for Chirps by author to work with our new users.
1. Add pages for logging in as a user
1. Update pages to limit creating, updating, and deleting Chirps to it's user.

This section was heavily inspired by this [RailsCast](http://railscasts.com/episodes/250-authentication-from-scratch).

## Adding a users "`model`"

### Enabling our app to keep passwords safe

> Discuss with your group what is needed from you when you log in to Facebook, Twitter, or Instagram.

When you put in your password, the web app does not save the password as is into the database.  Putting the password exactly as you type it into the database would make it very easy for anyone who has access to the database to know your password.  Commonly, the app instead makes a random secret string or a [salt](https://en.wikipedia.org/wiki/Salt_(cryptography), and your password encoded with the unique secret salt.  This way, when you log in, the app:

1. takes what you type in,
1. encodes it with the salt, and then
1. checks whether or not it matches the saved encode password

We'll be using the *bcrypt-ruby* `gem` in our project. If you're curious how it works, check out the [readme for the gem](https://github.com/codahale/bcrypt-ruby#how-bcrypt-works).  We add the gem by opening our `Gemfile` and adding to the bottom:

```
gem "bcrypt-ruby", :require => "bcrypt"
```

Now, our app is ready to guard our users' passwords!

### Make a user model

We tell our app about users by asking Rails to generate the model user in the console.

```bash
$ rails generate model user email:string password_salt:string password_hash:string name:string
```

The `password_salt` will hold the secret string, and the `password_hash` will hold the encoded password with the salt.

### Customize the user model

We can customize our user model so that when we create a user, it will take the password and save a newly generated salt and the hashed password.

In `app/models/user.rb`, we can customize the model like so:

```ruby
class User < ActiveRecord::Base
  attr_accessible :email, :password
  
  attr_accessor :password
  before_save :encrypt_password
  
  validates_confirmation_of :password
  validates_presence_of :password, :on => :create
  validates_presence_of :email
  validates_presence_of :name
  validates_uniqueness_of :email
  
  def self.authenticate(email, password)
    user = find_by(email: email)
    if user && user.password_hash == BCrypt::Engine.hash_secret(password, user.password_salt)
      user
    else
      nil
    end
  end
  
  def encrypt_password
    if password.present?
      self.password_salt = BCrypt::Engine.generate_salt
      self.password_hash = BCrypt::Engine.hash_secret(password, password_salt)
    end
  end
end
```

> Discuss this code with your group.  When does `encrypt_password` run?.

## Seeding the database

Rails has a nice way for us to ["seed" a database](http://guides.rubyonrails.org/active_record_migrations.html#migrations-and-seed-data) with some initial values in the `db/seeds.rb`.  Below is an example of seeding the database with users named Big Bird, The Early Bird, Word, Tweety Bird, and Melodie all with the password "changeme".


```ruby
authors = [{
  :name => 'Big Bird',
  :email => 'bigbird@example.com',
  :password => 'changeme'
}, {
  :name => 'The Early Bird',
  :email => 'theearlybird@example.com',
  :password => 'changeme'
}, {
  :name => 'Word',
  :email => 'word@example.com',
  :password => 'changeme'
}, {
  :name => 'Tweety Bird',
  :email => 'tweetybird@example.com',
  :password => 'changeme'
}, {
  :name => 'Melodie',
  :email => 'melodie@example.com',
  :password => 'changeme'
}]

User.create!(authors)
```

Add something similar to your `db/seeds.rb` and then run this following command in your console:

```bash
$ rake db:seed
```

Let's check if our users are in there!

```bash
$ rails console
```
```rb
> User.all
```

## Linking Chirp and User models to each other

<!-- ## Giving Users a login

## Updating routes to work -->

