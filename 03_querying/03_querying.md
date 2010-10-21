!SLIDE

# Querying for Data #

!SLIDE

# Map/Reduce #

!SLIDE

# Map transforms data #

!SLIDE

# Reduce aggregates data #

!SLIDE bullets incremental

# In CouchDB #

* Map generates lookup keys
* Keys point to a document
* Keys can have additional values

!SLIDE javascript

# Find by Title #

    @@@ javascript
    function(doc) {
      emit(doc.title, null);
    }

!SLIDE javascript

# Find only Posts by Title #

    @@@ javascript
    function(doc) {
      if (doc.type == "Post") {
        emit(doc.title, null);
      }
    }
!SLIDE javascript

# Find by Tags #

    @@@ javascript
    function(doc) {
      for(var idx in doc.tags) {
        emit(doc.tags[idx], 1)
      }
    }

!SLIDE

# Reduce #

    @@@ javascript
    function(keys, values, rereduce) {
      return sum(values);
    }

!SLIDE small

# Getting that data #

    /rubyenrails/_design/posts/_view/by_tag?key="riak"

    {"rows":[
    {"key":null,"value":2}
    ]}
    
!SLIDE small

## Only reduces based on the key ##

* Assumes `reduce=true`

!SLIDE small

# Include documents #

    /rubyenrails/_design/posts/_view/by_tag?key="riak"&include_docs=true&reduce=false
    {"total_rows":4,"offset":2,"rows":[
    {"id":"1234567","key":"riak","value":1,"doc":{"_id":"1234567","_rev":"6-2fd88529191482b8cebfe9136dbda4a1","title":"Why Riak Search Matters...","tags":["riak","full text"],"_attachments":{"attachment.png":{"content_type":"application/x-www-form-urlencoded","revpos":5,"length":36145,"stub":true}}}},
    {"id":"eb28b751a33d1bf9d7dfffd67001b5a0","key":"riak","value":1,"doc":{"_id":"eb28b751a33d1bf9d7dfffd67001b5a0","_rev":"1-b7bbd1aff51247a80653147b407d76c7","title":"Why I Am Excited About Riak Search","tags":["riak"]}}
    ]}
     
!SLIDE

# Complex Queries #

!SLIDE 
