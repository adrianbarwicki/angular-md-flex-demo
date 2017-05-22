# angular-md-flex-demo
## Solution for Safari vs. other engines

*** Proposal for hybrid approach (responsive and flex combined) ***
1. Use style="height:x%" for flex="x" in column layouts
2. Use style="width:x%" for flex="x" in row layouts
3. Shrink containers have flex="noshrink" attribute
4. Every "grow" container with standalone "flex" attribute should have layout-fill

***Constrains / Best practices***

1. No grow contents in shrink contents
Don't:
```
    <div layout="column">
        <div layout="column" flex>

        </div>
    </div>
```

2. No nested shrink contents
Don't:
```
    <div layout="column">
        <div layout="column">
        </div>
    </div>
```

2. The relative heights must always add up to 100%.
Don't:
```
    <div layout="column" flex>
        <div layout="column" style="height: 20%"></div>
        <div layout="column" style="height: 20%"></div>
    </div>
```
Do:
```
    <div layout="column" flex>
        <div layout="column" style="height: 50%"></div>
        <div layout="column" style="height: 50%"></div>
    </div>
```

3. Shrink containers must not be scrollable
Don't:
```
    <md-content layout="column">
    </md-content>
```
Do:
```
    <md-content layout="column" flex>
    </md-content>
```

4. Scrollable containers must not contain any contents of "row" / "Horizontal" layout
Don't:
```
    <md-content layout="column">
         <div layout="row" flex>
            ...
         </div>
          <div layout="row" flex>
            ...
          </div>
    </md-content>
```
Do:
```
    <md-content layout="column" flex>
         <div layout="column" flex="noshrink"></div>
         <div layout="column" flex="noshrink"></div>
    </md-content>
    <md-content layout="column" flex>
         <div layout="column" flex="noshrink"></div>
    </md-content>
```

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

***OK: test11.html***
Fixed flex % containers are nested and contain grow containers that should devide the space equally between them. There are alsoc scrollable.

***NOT OK: test12.html***
Scrollable containers do not work with "row" / horizontal containers

***OK: test13.html***
Scrollable containers do work with "column" / vertical containers
Constrain for children of scrollable containers:
```
<div layout="column" flex="noshrink" class="red">
    <h1>[3 Test in shrink container]</h1>
    <h1>[3 Test in shrink container]</h1>
    <h1>[3 Test in shrink container]</h1>
</div>
```
* must have the flex="noshrink" property
* must be of column layout

***OK: test14.html***
Horizontal containers work well

***OK: test15.html***
Nested Horizontal containers work well

***OK: test16.html***
test15 combied with test13