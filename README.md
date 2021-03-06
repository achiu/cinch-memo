Cinch-Memo
===========

The Cinch Memo Plugin. Store messages for users while they are away.

Installation
---------------------

if you haven't already...

    $ gem install cinch
    
then install this gem.

    $ gem install cinch-memo

Installation and Setup
----------

#### Configuration ####

To setup the plugin to work with your cinch bot, we'll need to provide some info like so:

    Cinch::Plugins::Memo::Base.configure do |c|
      c.store   = :redis          # data store
      c.host    = 'localhost'     # your host
      c.port    = '6709'          # your port
    end

Currently, only Redis is available as a backend store.

#### Commands ####

  * !memo [nick] [message]    - stores the message for the user
  * !memo?                    - returns memo's for your nick

The bot will also auto message a user on join of the channel if there are messages for that user.
  
## Integration with Cinch ##

It's simple. follow the guide on cinch or do something like:
    
    # mybot.rb
    require 'cinch'
    require 'cinch/plugins/memo'

    Cinch::Plugins::Memo::Base.configure do |c|
      c.store   = :redis          # data store
      c.host    = 'localhost'     # your host
      c.port    = '6709'          # your port
    end

    bot = Cinch::Bot.new do
      configure do |c|
        c.server           = "irc.freenode.net"
        c.nick             = "cinch"
        c.channels         = ["#padrino"]
        c.plugins.plugins  = [Cinch::Plugins::Memo::Base]
      end

    end

    bot.start

Finally, run your bot.

    ruby -rubygems mybot.rb

And there you go!


TODO
-----

  * add auto deliver message functionality when you sign on.
  * add rate limiting ability
  * add additional backend stores.
  * add some kind of auth mech
