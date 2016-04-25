# Beautifying your page with Bootstrap

Right now, Chirper can do a lot, but it looks a little plain.

Using `css` we can completely change the way it looks.  There are some styles that get written and used over an over again.  Luckily for us, these common styles have been put into a `css` framework called "Bootstrap" and Rails happens to have a `gem` for it.

[https://github.com/seyhunak/twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails)

We are going to need some outside help for this one! In order to chirp our latest fashion images, we'll need to use a new `gem`.

## Adding Bootstrap

Let's add the `gem` "bootstrap" to our project. First, we need to open our `Gemfile` and add to the bottom:

```rails
gem 'sprockets', '~> 3.0'
gem 'bootstrap-sass', '~> 3.3.1'
gem 'bootstrap', '~> 4.0.0.alpha3'
```
Save the file and then type in the command line:

```bash
$ bundle install
```
`Bundler` will now install bootstrap into our project.

Bootstrap uses Sass (Syntactically Awesome Style Sheets) rather than Cascading Style Sheets. We need to change our style sheet extension in app/assets/stylesheets/application.css.

We could do this in Sublime Text, but let's try using the command line instead! We just run:

```bash
mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
```
Now we can add bootstrap styles in our app/assets/stylesheets/application.css file:

```
@import "bootstrap-sprockets";
@import "bootstrap";
```

Let's see what has changed! We can take a look at the changes to our project here: [http://localhost:3000/chirps/new](http://localhost:3000/chirps/new)

> This would be a great time to discuss `bootstrap` and `sass`  with your coach. 
