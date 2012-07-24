---
layout: post
title: No Python switch statement?
tags:
- Python
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: ''
  sfw_comment_form_password: PP4b4DdFlgdb
---
When I was relatively new to Python and writing my first real program, one of the first things I noticed was the lack of a switch statement, which had become commonplace when coding in Java.

Since then I've found multiple ways to achieve the same effect (without the use of if-else's!);

Firstly the concept of <strong>assigning a variable</strong> using a switch, which in Java may look something like this;

<pre lang="java" line="1">
  int result;
  switch(condition)
   {
     case 'a': result = 1; 
       break;
     case 'b': result = 2; 
       break;
     case 'c': result = 3;  
       break
     default: result = 0;
   }
</pre>

We can achieve the same in Python using a dictionary;

<pre lang="python" line="1">
result = {
  'a': 1,
  'b': 2,
  'c': 3
}[condition]
</pre>

And lets say we want to define functions as the result of our switch. Also you may have noticed that the above does not define a default action, which is present in the Java equivalent. We can include both like so;

<pre lang="python" line="1">
# define the dict
values = { 
           'a': do_stuff, 
           'b': do_stuff2, 
           'c': do_stuff3,
 }
# get the function
values.get(condition, do_default)()
</pre>

This will execute the do_stuff function defined by the condition, and if a value is not found then it will execute do_default.

Much less verbose wouldn't you say?

I have one more to add to the list, which I guess is really Reflection, but can be used for the same purpose and is pretty cool in Python. 

<pre lang="python" line="1">
method_name = 'do_' + condition
if not hasattr(self, method_name):
   do_default
else:
   method = getattr(self, method_name)
   result = method()

def do_a:
  return 1
def do_b:
  return 2
def do_c:
  return 3
def do_default:
  return 0
</pre>

Some explanation may be in order if you're not familiar with Python. If you're a Java pro, then you may be used to fetching attributes or methods using the getClass() function. This is much easier and awesome in Python. 

To put it bluntly, the built in function <a href="http://docs.python.org/library/functions.html#hasattr">hasattr</a> checks the object's (in this case 'self') attributes for the given string. 
Then we use <a href="http://docs.python.org/library/functions.html#getattr">getattr</a> to retrieve the attribute, in this case a function, which is then executed.


   
There you have it. As you see, these examples of switch statements provide much more flexibility (mainly in the fact that you are not limited to primitive types!), and are in most cases much less verbose.
Happy coding!
