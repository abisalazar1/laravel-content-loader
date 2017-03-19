# laravel-content-loader
jQuery Laravel Content Loader


Default Options

```
  url: "/load",   
  data : {}, 
  csrfToken:$('meta[name="csrf-token"]').attr('content') || Laravel.csrfToken, 
  auto: true, 
  ajaxType : "GET",
  contentDataType: null, 
  lastPage : null,  
  results: '#' + $(this).attr('id') + "_results", 
  response: function (response) { 
     alert("You must add a response function."); 
  },
  error: function (error) { 
      console.log(error);
  }

  url : // Url to be hit by the ajax request
  data : // Data to be send with the ajax request
  csrfToken: // By default this will look for a csrf-token in a meta tag or a javascript global varible.
  auto: // By default as soon as it's called this will perform an ajax request to load to grab the first load of data
  ajaxType :  // Ajax is set to perform a GET request.
  contentDataType : // This will be added to the data params. 
  results: // This will add an easier way to manupulate the results.
  response: // this is a mandatory field that you need to send in order to manipulate your data.
  error: // By default, it will console log the error if anything goes wrong with the request.

```


Basic Use:

```
 $('#userLoader').contentLoader({
                response: function (response) {
                   // Your amazing code here.
                }
            });
            
```



Example Use:


```
    // JavaScript
    
    $('#userLoader').contentLoader({
                contentDataType: "users",
                response: function (response) {
                    response.data.forEach(function (obj) {
                        $(this.results).append("<li>"+obj.name+"</li>");
                    }.bind(this));
                }
            });
            
            
            $('#postLoader').contentLoader({
                contentDataType: "posts",
                response: function (response) {
                    response.data.forEach(function (obj) {
                        $(this.results).append("<li>"+obj.body+"</li>");
                    }.bind(this));
                }
            });


      //Route
      Route::get('/load', function (){
          if(\Request::exists('users')){
              return response(User::paginate(15));
          }else{
             return response(Post::paginate(10));
          }
      });
      
      
      
      // HTML 
      
          <div class="content">
                <div class="title m-b-md">
                    Laravel Loader
                </div>
                <ul id="userLoader_results">

                </ul>
                <button id="userLoader">Load More</button>
                
                <br>
                <ul id="postLoader_results">


                </ul>

                <button id="postLoader">Load More</button>

            </div>
```
