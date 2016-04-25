# Let's change how Chirper looks

Now that we've installed Bootstrap, we can make even more changes to the way our page uses using Bootstrap's classes.

We can check out Bootstrap's styles here:

[https://getbootstrap.com/css/](https://getbootstrap.com/css/)

Let's add navigation, so we can see what pages are available.

We can see that Bootstrap has already put together a navbar we can use. We can take a look at the navbar components they have made here:

[https://getbootstrap.com/components/#navbar](https://getbootstrap.com/components/#navbar)

Let's use their default navbar:

```
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Brand</a>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#">Link <span class="sr-only">(current)</span></a></li>
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">One more separated link</a></li>
          </ul>
        </li>
      </ul>
      <form class="navbar-form navbar-left" role="search">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
```

We have a special file in views that lets us add html that changes all our pages. Let's paste that html after our `<body>` tag in `app/views/layouts/application.html.erb`.

![http://imgur.com/gJvKEZE](http://imgur.com/gJvKEZE)

Now we can go to any of our pages, and we should be able to see our navbar at the top of the screen. Check it out:

[http://localhost:3000/](http://localhost:3000/)

[http://localhost:3000/chirps/new](http://localhost:3000/chirps/new)

Let's customize it! We can change

`<a class="navbar-brand" href="#">Brand</a>` to 
`<a class="navbar-brand" href="/">Chirper</a>`