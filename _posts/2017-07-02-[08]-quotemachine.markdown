---
layout: post
title:  quotemachine[JS]
date:   2017-07-02
categories: javascript
---

Below was written while working on the quote machine user stories from [FCC](https://freecodecamp.org). Actually had this draft sitting all lonesome for awhile so post date used is a give or take. Below are my notes.

Reminder Note: I initially created this as a rails app with plans of inputting/saving quotes in addition to fetching my stoic quotes.

- - - 

upon creating rails app/creating initial DB...

```
[Web Dev]:  /vagrant/src/quotemachine $ rake db:create:all
The PGconn, PGresult, and PGError constants are deprecated, and will be
removed as of version 1.0.

You should use PG::Connection, PG::Result, and PG::Error instead, respectively.

Called from /home/vagrant/.rvm/gems/ruby-2.3.1/gems/activesupport-4.2.6/lib/active_support/dependencies.rb:240:in `load_dependency'
```

```
[Web Dev]:  /vagrant/src/quotemachine $ rvm -v
rvm 1.27.0 (latest) by Wayne E. Seguin <wayneeseguin@gmail.com>, Michal Papis <mpapis@gmail.com> [https://rvm.io/]
```

```
[Web Dev]:  /vagrant/src/quotemachine $ ruby -v
ruby 2.3.1p112 (2016-04-26 revision 54768) [i686-linux]
```

```
[Web Dev]:  /vagrant/src/quotemachine $ rails -v
Expected string default value for '--rc'; got false (boolean)
Rails 4.2.6
```

[SO Post](https://stackoverflow.com/questions/44607324/installing-newest-version-of-rails-4-with-postgres-the-pgconn-pgresult-and-p/44607369#44607369)

I noticed the same deprecation warnings when upgrading from `pg 0.20.0` to `pg 0.21.0`. I didn't seem to have any actual problems with pg and my apps (dev, staging, and production) all seemed to work fine.

I found the warning annoying, however, so I locked all my Gemfiles at `pg 0.20.0`.

Added `gem 'pg', '~> 0.20.0'` to Gemfile and eliminated this warning as well. Originally, Rails tried to use 0.21.0

- - - 
7/10

put a `test.json` file on AWS S3 -- direct link at first was not working, until made public
put in link as getJSON(); request-- looking at network shows link as button pressed, but nothing else

also showing error `SyntaxError: JSON.parse: unexpected end of data at line 1 column 1 of the JSON data`

[JS w/ RAILS](http://edgeguides.rubyonrails.org/working_with_javascript_in_rails.html)

Thinking I need to create a table in order to pipe api call--
[generating a model will create table](http://guides.rubyonrails.org/active_record_migrations.html)

`$ rails generate model quote saying:text author:string`

^ creates quote model and Quotes table with saying and author-- using text for saying so theres no cap to characters (it happened b4 and i had to change the table from string to text)

^ with table created, im thinking to edit controller 

[RoR GUIDES](http://guides.rubyonrails.org/)

- - - 
7/11

adding `?callback=?` to the end of the json link brought up obj on dev tools panel
got rid of ERROR `SyntaxError: JSON.parse: unexpected end of data at line 1 column 1 of the JSON data`

^ thank you [JSON SO Post](https://stackoverflow.com/questions/5943630/basic-example-of-using-ajax-with-jsonp)

** present problem: is the info actually showing up on browser when button pressed

- - - 

finally got it working-- 
the controller and table will be great to give add quote functionality, but unneccessary for api request

what i needed was to add $ajax([]) 

testing this while making another quotemachine using forismatic api and not just a file I created on my own--
it became apparent that trying to use $getJSON() was not going to work 

SN: I went with making my own file because I wanted specific Stoic Quotes and not just w.e quote-- although the quotes that come through using forismatic are pretty great /endSN


