# CSS

## Table of Contents

1. [BEM](#bem)
2. [Preprocessing & Source Maps](#preprocessing--source-maps)
3. [Box Sizing](#box-sizing)
4. [Grids & Frameworks](#grids--frameworks)
5. [Prefixes](#prefixes)
6. [Selector Chains](#selector-chains)
7. [Flexbox](#flexbox)
8. [Help](#help)

## BEM
We highly encourage using BEM conventions. You can read more about it [here](http://getbem.com/).


## Preprocessing & Source Maps
SCSS, configured to compressed. Do not use Compass. You can find a Gruntfile.js and package.json preconfigured in the [Skeleton repo](https://github.com/brightbrightgreat/skeleton).

Please make sure you keep your source maps up to date on the server at the end of every day.

## Box Sizing
Use box-sizing: border-box; on everything. This is already included in the startup SCSS files in the [Skeleton repo](https://github.com/brightbrightgreat/skeleton).


## Grids & Frameworks
Do not use frameworks like Bootstrap, if you want to have a grid framework, we'd prefer something like [this](https://css-tricks.com/dont-overthink-it-grids/).


## Prefixes
Use Autoprefixer for prefix management. (Browser support string: last 3 versions). This is already set up in the grunt-related files in the [Skeleton repo](https://github.com/brightbrightgreat/skeleton).


## Selector Chains
Do not nest selector chains more than 3 levels ie: `.module .box .title` is acceptable, but `.module .box .title span` is not. The fewer levels the better. 

Pseudo elements and classes do not count as an extra level when attached to a selector ie: `.box:before` is one level, `.box :before` is two - although I don’t ever foresee the second example being useful. 

If you need more than three levels, it’s time to refactor. 

Use `@extend` judiciously. Favor adding more classes to HTML over using `@extend` in your stylesheet.


## Flexbox
We highly encourage the use of flexbox . Autoprefixer makes it very easy to use, code with the modern syntax and let Autoprefixer do the rest. [This guide has more information if needed](https://css-tricks.com/snippets/css/a-guide-to-flexbox/). 

## Help 
If you have any questions, please contact Tiffany Stoik [tiffany@brightbrightgreat.com](mailto:tiffany@brightbrightgreat.com).
