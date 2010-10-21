!SLIDE

# CouchDB and Ruby #

!SLIDE ruby

    @@@ ruby
    uri = URI.parse('http://localhost:5984/rubyandrails')
    response = Net::HTTP.get(uri)
    # => String

!SLIDE

# Done! #

!SLIDE

# Too low-level? #

!SLIDE bullets incremental

* Abstracts HTTP
* Turns JSON into Hashes

# CouchRest #

!SLIDE ruby

    @@@ ruby
    CouchRest.get('http://localhost:5984/rubyandrails')
    # => Hash

!SLIDE

# Still too low-level? #

!SLIDE

# CouchPotato #

* Maps Documents to Objects
* Generates View code

!SLIDE ruby

    @@@ ruby
    require 'couch_potato'
    class Post
      include CouchPotato::Persistence
      
      property :published_at, :type => Date
      property :title
      property :tags
    end

!SLIDE ruby small

    @@@ ruby
    post = Post.new(
      :title => "Why Riak Search Matters...")

    CouchPotato.database.save(post)

!SLIDE

# Views with CouchPotato #

!SLIDE ruby small

    @@@ ruby
    class Post
      view :by_title, :key => [:title, :published_at]
    end

    CouchPotato.database.view(Post.by_title)

!SLIDE

# Still too low-level? #

!SLIDE

# SimplyStored #

* ActiveRecord-ish
