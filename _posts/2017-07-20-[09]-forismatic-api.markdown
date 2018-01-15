---
layout: post
title:  "forismatic api [doc]"
date:   2017-07-20
categories: javascript, fcc
---

I've already completed a quote machine that was setup using a file I created with about 30 something quotes-- stoic quotes to be exact which I stored using AWS S3

Although, not exactly the same as using the forismatic API they both are similar enough in overall requirements

Which is why I decided to use it as a way to reinforce what learned while doing mine

- - - 

messing with forismatic api after making stoic quotemachine functional

get vagrant running

get into folder where you want project to live and create proj

check your config file

initial db (make sure you are already in project path)
`rake db:create:all`
if you don't do this you'll end up with 
`FATAL: database "quoteapi_development" does not exist` error on localhost page

if you havent already done so, fire up that server in a seperate window
you should see a welcome aboard page :)

setup your git 

added rails_12factor gem and edit prod.rb file to allow fallback to assets pipeline if precompile asset is missed

setup heroku

^ all that already in a blog post

- - - 

right now, there's nothing to see

you have no routes setup/ view/ controller

generate controller, setup something on view file to... view, and make sure you setup route to be able to view... the view.

check localhost page, w.e you put in the view file should show up :)

- - - 

off the bat I know I want an area where the quote/ author is going to show up
and a button so I make those in html

how I'm going to insert the quote in that div and what will make the button work will be done within the `<script></script>` tags

upto this point: 

```
<script>
  $(document).ready(function() {              // page loads then...
    $("#quote").on("click", function() {      // this makes the button work
      $(".quotes").html("button works");      // this is what happens when button pressed, if it shows up, I know it works
    });
  });
</script>

<h1>testing...</h1>

<div class="quotes">
  <!-- Quote gets inserted here -->
</div>

<button id="quote">Quote</button>

```
now comes the hooking up the API-- this time I'm looking [here](http://forismatic.com/en/) under API section

reading through, API requests are sent in HTML format to this link http://api.forismatic.com/api/1.0/

if put that link as is in the browser, you get `Error: wrong method.`

if you continue reading through and check out the query example, putting
?method=getQuote&key=457653&format=xml&lang=en at the end of http://api.forismatic.com/api/1.0/ will bring up information
quote, author and other things

i want json so I change where it says format=xml to format=json, shows the same info as before, but in json format
when you do that you see format change

- - - 

back to the script:
using `$.getJSON()` wasn't working for me, instead went to use ajax in order to put settings and such
with below script, using the dev tools I can see the request is successful, but nothing is showing up in response... yet

```
<script>
// jQuery.getJSON( url [, data ] [, success ] )
// jQuery.ajax( url [, settings ] )

  $(document).ready(function() {
    $.ajax({
      url: "http://api.forismatic.com/api/1.0/",
      data: {
        method: "getQuote",
        format: "jsonp",
        lang: "en",
        jsonp: "jsonp"   
      },
      success: function(data) {
        $(".quotes").html(data);
      }
    });
    
    // $("#quote").on("click", function() {
    //   $(".quotes").html("button works");
    // });

  });
</script>

<h1>testing...</h1>

<div class="quotes">
  <!-- Quote gets inserted here -->
</div>

<button id="quote">Quote</button>

```

back to script:
turns out I needed to move `jsonp: "jsonp"` outside of `data` 
and then declare that as the dataType
once I did that it showed up under response tab in dev tools side panel

I then went ahead assigned varaiables to data I wanted to isolate (quoteText & quoteAuthor) in order to show them as html 
which shows up in browser [success!]

```
<script>
// jQuery.getJSON( url [, data ] [, success ] )
// jQuery.ajax( url [, settings ] )

  $(document).ready(function() {
    
      $.ajax({
        url: "http://api.forismatic.com/api/1.0/",
        jsonp: "jsonp",     // w/o this dataType doesnt work, it gives error (gist: `...blocked due to MIME type mismatch`)
        dataType: "jsonp",
        data: {
          method: "getQuote",
          format: "jsonp",
          lang: "en"  
        },
        success: function(data) {
          var quote = data.quoteText;
          var author = data.quoteAuthor;
           $(".quotes").html(quote + author);
        }
      });
 
    
    // $("#quote").on("click", function() {
    //   $(".quotes").html("button works");
    // });

  });
</script>

<!--h1>testing...</h1-->

<div class="quotes">
  <!-- Quote gets inserted here -->
</div>
<br />

```
next:
I'd like to put quotations and address the missing authors on some quotes

back to script:
below has quotes showing up addressing issues mentioned above

```
<script>
// jQuery.getJSON( url [, data ] [, success ] )
// jQuery.ajax( url [, settings ] )

  $(document).ready(function() {
      $.ajax({
        url: "http://api.forismatic.com/api/1.0/",
        jsonp: "jsonp",
        dataType: "jsonp",
        data: {
          method: "getQuote",
          format: "jsonp",
          lang: "en"  
        },
        success: function(data) {
          var quote = data.quoteText;
          var author = data.quoteAuthor;

          var showAll = "";
          showAll += "\"" + quote + "\"" + " -" + author;

          if(author) {
            $(".quotes").html(showAll);
          }
          else {
            $(".quotes").html(showAll + "Unknown");
          }
           
        }
      });
  
    // $("#quote").on("click", function() {
    //   $(".quotes").html("button works");
    // });

  });
</script>

```
next: button funtionality 
I've put ajax req inside a function to be called on page load 
and then call that same function within button/selector

this way quote shows up on page loadup with quote change functionality upon button press

```
<script>
// jQuery.getJSON( url [, data ] [, success ] )
// jQuery.ajax( url [, settings ] )

  $(document).ready(function() {
    
    function newQuote() {
      $.ajax({
        url: "http://api.forismatic.com/api/1.0/",
        jsonp: "jsonp",
        dataType: "jsonp",
        data: {
          method: "getQuote",
          format: "jsonp",
          lang: "en"  
        },
        success: function(data) {
          var quote = data.quoteText;
          var author = data.quoteAuthor;

          var showAll = "";
          showAll += "\"" + quote + "\"" + " -" + author;

          if(author) {
            $(".quotes").html(showAll);
          }
          else {
            $(".quotes").html(showAll + "Unknown");
          }
           
        }
      });
   }
   newQuote(); 
    
    $("#quote").on("click", function() {
      newQuote();
    });

  });
</script>

```

at this point: 
there is no styling, no tweet ability, just quote functionality

add another button, for tweeting this time
as well as selector to connect to the button giving it that clicking functionality

```
<script>
// jQuery.getJSON( url [, data ] [, success ] )
// jQuery.ajax( url [, settings ] )

$(document).ready(function() {
  
  var showAll;

  function newQuote() {
    $.ajax({
      url: "http://api.forismatic.com/api/1.0/",
      jsonp: "jsonp",
      dataType: "jsonp",
      data: {
        method: "getQuote",
        format: "jsonp",
        lang: "en"  
      },
      success: function(data) {
        var quote = data.quoteText;
        var author = data.quoteAuthor;

        showAll = "";
        showAll += "\"" + quote + "\"" + " -" + author;

        if(author) {
          $(".quotes").html(showAll);
        }
        else {
          $(".quotes").html(showAll + "Unknown");
        }
           
      } //success end
    }); //ajax end
  } //newQuote func end
  newQuote(); 
    
  $("#quote").on("click", function() {
    newQuote();
  });

  $("#tweet").on("click", function() {
    // var windowObjectReference = window.open(strUrl, strWindowName, [strWindowFeatures]);
    // https://dev.twitter.com/web/tweet-button/web-intent
    window.open("https://twitter.com/intent/tweet?text=" + showAll + " &hashtags=quotes");
  })

}); //end
</script>

```

now all that is left would be to shorten tweet too long to tweet**

SN: issue in pushing up to repo--

  Viewing Unpushed Git Commits

  git log origin/master..HEAD

  You can also view the diff using the same syntax

  git diff origin/master..HEAD


something else I found helpful-- 
[SO POST](https://stackoverflow.com/questions/2514270/how-to-check-for-changes-on-remote-origin-git-repository)

  
  You could `git fetch origin` to update the remote branch in your repository to point to the latest version. For a diff against the remote:

  `git diff origin/master`

  Yes, you can use caret notation as well.

  If you want to accept the remote changes:

  `git merge origin/master`

was not able to exit of bash cmd, used: * perhaps look into a better way to do this
  
  You can always try the obvious things like ^C, ^D (eof), Escape etc., but if all fails I usually end up suspending the command with ^Z (Control-Z) which puts me back into the shell. 

Z worked.


