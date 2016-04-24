# Beautifying your page with Bootstrap

We are going to need some outside help for this one! In order to chirp our latest fashion images, we'll need to use a new `gem`.

## Adding Bootstrap

Let's add the `gem` "bootstrap" to our project. First, we need to open our `Gemfile` and add to the bottom:

```rails
gem 'bootstrap', '~> 4.0.0.alpha3'
```
Save the file and then type in the command line:

```bash
$ bundle install
```
`Bundler` will now install bootstrap into our project.

Bootstrap uses Sass (Syntactically Awesome Style Sheets) rather than Cascading Style Sheets. We need to change our style sheet extension in app/assets/stylesheets/application.css.

We could do this in Sublime Text, but let's try using the command line instead!

We can use `mv`, the move command, to rename application.css. We just run:

```bash
mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
```
Now we can add bootstrap styles in our app/assets/stylesheets/application.css file:

```
@import "bootstrap";
```

> This would be a great time to discuss `bootstrap` and `sass`. with your coach. 
