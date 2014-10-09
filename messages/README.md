# What should messages have?

> What does a message need to have?
>
> Let's discuss!
>
> For example, a message should have an author, a message body...what are some other things?






# Let's make some messages!

Let's command Rails to work with these kinds of messages:

~~~
$ rails generate model Message body:text author:string chirp_time:date
~~~

Rails will now make something called a "`model`" to represent this idea of the message.
