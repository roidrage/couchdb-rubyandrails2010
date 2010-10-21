!SLIDE

# CouchDB and Ruby #

!SLIDE ruby small

    @@@ ruby
    uri = URI.parse('http://localhost:5984/rubyandrails')
    response = Net::HTTP.get(uri)
    # => String

!SLIDE

# Done! #

!SLIDE

# Too low-level? #

!SLIDE bullets incremental

# CouchRest #

* Abstracts HTTP
* Turns JSON into Hashes


!SLIDE ruby small

    @@@ ruby
    CouchRest.get('http://localhost:5984/rubyandrails')
    # => Hash

!SLIDE

# Still too low-level? #

!SLIDE bullets incremental

# [CouchPotato](http://github.com/langalex/couch_potato) #

* Maps Documents to Objects
* Generates View code
* Based on CouchRest

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

!SLIDE bullets incremental

# [SimplyStored](http://github.com/peritor/simply_stored) #

* ActiveRecord-ish
* Support for associations
* Based on CouchPotato

!SLIDE ruby small

    @@@ ruby
    class Post
      include SimplyStored::Couch
      property :title
      has_one :author
    end

!SLIDE ruby small

    @@@ ruby
    post = Post.new(
      :title => "Why Riak Search Matters...",
      :author => Author.new(:name => "Mathias"))
    
    post.save

!SLIDE ruby small

    @@@ ruby
    Post.find_by_title("Why Riak Search Matters...")
    # => <Post#eb28b751a title: "Why Riak..."

    Post.find_all_by_tag("riak")
    # => [<Post...>, <Post...>]
