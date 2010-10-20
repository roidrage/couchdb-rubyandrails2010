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

# Find by Tags #

    @@@ javascript
    function(doc) {
      for(var idx in doc.tags) {
        emit(doc.tags[idx], 1)
      }
    }

!SLIDE

# Complex Queries #

!SLIDE 
