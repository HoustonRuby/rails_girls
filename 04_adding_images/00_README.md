# What if I want to Chirp images?

We are going to need some outside help for this one! In order to chirp our latest fashion images, we'll need to use a library. In Rails we call these `gems`.

## Adding paperclip

Let's add paperclip to our project. First, we need to open our `Gemfile` and add to the bottom:

```rails
gem "paperclip", "~> 4.2"
```

Save the file and then type in the command line:

```bash
$ bundle install
```
`Bundler` will now install paperclip into our project.

> While that's installing, This would be a great time to discuss with your coach `bundler` and the `Gemfile`. If you didn't get a chance to earlier, you should also talk about what a `gem` is.

