mixin-media-queries-oocss
=========================

Using SASS mixins to include breakpoints inside modules

#The problem
Following the typical structure:
- Base
- Layout
- Modules
- Breakpoints
- …

We have the media queries in different files. This is not the better OOCSS approach since it is desirable to have all the properties of a module grouped together.
Example:
We have our module in the folder css/modules/module.scss:
```
.module {
    display: block;
}
```
If we want it to display inline at a given screen width we would have this module declared again in css/breakpoints/bp2.scss (for example):
```
@media only screen and (min-width: 30em) {
    […]
    
    .module {
        display: inline;
    }
    
    […]
    
}
```
It would be better if we have this declaration in the same module file (module.scss):
```
.module {
    display: block;
    @media only screen and (min-width: 30em) {
        display: inline;
    }
}
  ```  
Giving as a result:
```
.module {
    display: block;
}
@media only screen and (min-width: 30em) {
    .module {
        display: inline;
    }
}

```
#A solution
We can create a SASS mixin to make it easier to write these media queries and make use of our varibles configuration.
__The mixin__
```
@mixin responsive($breakpoint) {
	
	@media only #{$media} and ($feature: $breakpoint) { //$feature: min-width as set in variables.scss
		@content;
	}
	

}
```
__The mixin in action__
```
.module {
	display: block;
	@include responsive($bp2){ //$bp2: 30em as set in variables.scss
		display: inline;
	}
}
Giving as a result:
.module {
  display: block; }
  @media only screen and (min-width: 30em) {
    .module {
      display: inline; } }
```
 

