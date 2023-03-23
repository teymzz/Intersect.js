# Intersect.js 
This is an advanced level plugin that is built upon javascript IntersectionObject and the window scroll event 

#### Initialization 
```js
let intersect = new Intersect;
```

#### Methods 
This plugin has three different methods that helps to detect intersection which are listed below 

   + ```observe()``` used for observing elements
   + ```status``` used for handling elements using predefined options for _intersect_ or _onScroll_
   + ```onScoll``` used for handling a more advanced scroll event 

##### Working with _observe()_ method 
This method behaves like the normal IntersectionObserver. The sample of usage is shown below 

   ```js 
   let intersect = new Intersect;

   intersect.observe({
        
        el: '.setup',

        callback: (entry, observer) => {

           if(entry.isIntersecting)  observer.unobserve(entry.target)

        }

   });
   ```
When working with ```Intersect``` methods, the option supplied must be provided with a selector name using the key ```el``` and a ```callback()``` function. The callback function enables us to access each target element and the intersection observer itself. It also provides a shorter method for the _IntersectionObserver_ ```isIntersecting``` key which is ```inview```. The sample above will select all classes with value of _setup_ and observe each element. While the sample code above is accepted, we can also rewrite the code in a shorter form as shown below:

   ```js 
   let intersect = new Intersect;

   intersect.observe({
        
        el: '.setup',

        callback: (entry) => {

           if(entry.inview)  entry.unobserve() ;

        }

   });   
   ```

##### Working with _status()_ method 
This method is similar to _observe()_ method but with a slight difference as it provides more functionality of scroll event through options. A sample code is shown below

   ```js 
   let intersect = new Intersect;

   intersect.status({
        
        el: '.setup',

        onScroll: 'intersect', 

        callback: function(entry) {

            if(entry.inview) entry.unobserve();

        }

   });
   ```
The ```status``` method provides an additional key ```onScroll``` which determines if a scroll event is applied or just a normal intersection. The options accepted option is either ```[scroll|intersect]```. The sample code above is handled in a more advanced way as the ```entry``` argument provides us access to more keys which are listed below: 
   

   + ```id``` the id of the target entry element if defined
   + ```scrollPoint``` current window's scroll point
   + ```inview``` same as _isIntersecting_
   + ```element_ returns a data for the current object with the keys below
       + ```id``` the id of the target entry element if defined
       + ```fromWindowTop``` current distance of the entry element from the window's top.
       + ```aboveWindowTop``` returns true if the entry element is entirely above the window's top.
       + ```belowWindowTop``` returns true if part of the entry element is below the window's top.
       + ```zeroDownwards``` returns true if the distance of the element from the window's top is 0 or less than.
       + ```zeroUpwards``` returns true if the distance of the element from the window's top is 0 or greater than.
       + ```zeroPoint``` returns true if the distance of the element from the window's top is 0.

   > Note that When the _"scroll"_ option is used, the onscroll event is activated for the observer. When onscroll event is turned on, we can get to use the ```unobserved()``` method which helps to detect if an element has been unobserved. A sample is shown below: 

   ```js 
   let intersect = new Intersect;

   intersect.status({
        
        el: '.setup',

        onScroll: 'scroll', 

        callback: function(entry) {

            if(entry.inview) { 
                entry.unobserve(); 
                console.log(entry.target, ": has been removed from scroll list")
            } else {
             if(!entry.unobserved()){
                 console.log(entry.target, ": not in view");
             }
            }

        }

   });
   ```

   > In code above, since the _scroll_ option is supplied, the scroll event will be started. The code checks if the entry is in view then removes it from the scroll list through the ```entry.unobserve()``` method. This activity will also save the unobserved entry in a storage list. If the entry is not in view, it will go on to check if the element is not in the list of unobserved entries before printing the displaying the text "not in view" to the console



##### Working with _onScroll()_ method 
This method is similar to is a short syntax for the _scroll_ option's _onScroll:"scroll"_. An example is shown below: 


   ```js 
   let intersect = new Intersect;

   intersect.onScroll({
        
        el: '.setup',

        callback: function(entry) {

            if(entry.inview) { 
                entry.unobserve(); 
                console.log(entry.target, ": has been removed from scroll list")
            } else {
             if(!entry.unobserved()){
                 console.log(entry.target, ": not in view");
             }
            }

        }

   });
   ```


