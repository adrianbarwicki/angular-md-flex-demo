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

***OK: test5-noflex.html ***
We use explicit styles for heights in % and it has the correct behaviaur.
Minus of this approach: Grow / shrink not possible