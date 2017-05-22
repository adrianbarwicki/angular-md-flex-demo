# angular-md-flex-demo
## Solution for Safari vs. other engines

1. Use style="height:x%" for flex="x" in column layouts
2. Use style="width:x%" for flex="x" in row layouts
3. Every "grow" container with standalone "flex" attribute should have layout-fill


## Edge cases

***NOT OK: test3.html***
Fixed flex does not work properly in grow column container. Their height are based on screen size, not on parent size.

***NOT OK: test5.html***
Fixed flex containers in fixed flex containers. Their height are based on screen size, not on parent size. Same with test3.html.

***OK: test5-noflex.html***
We use explicit styles for heights in % and it has the correct behaviaur.
Minus of this approach: Grow / shrink not possible

***OK: test6.html***
Grow containers have always layout specifed. Fixed flex % is replaced with css rules.

***OK: test8.html***
Grow containers have always layout specifed. Fixed flex % is replaced with css rules, same with test6.html but with 3 containers of fixed % height.

***NOT OK: test9.html***
Grow containers have always layout specifed. Fixed flex % containers are nested and contain fixed flex % containers. The specific thing is that the containers as a specific level do not define the 100% height.
In this scenario, there are troubles with Safari and Chrome - Safari seems to ignore the specified 50% and takes the full height and Chrome seems to follow exactly what is specified in the css.

***OK: test10.html***
Fixed flex % containers are nested and contain grow containers that should devide the space equally between them.