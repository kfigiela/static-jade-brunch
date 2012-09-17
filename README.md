[![build status](https://secure.travis-ci.org/ilkosta/static-jade-brunch.png)](http://travis-ci.org/ilkosta/static-jade-brunch)

## static-jade-brunch
Adds [Jade](http://jade-lang.com) support to [brunch](http://brunch.io) without wrapping the compiled html in modules of type commonjs/amd. 
Each jade file that don't start with `_` (underscore) is compiled in `public/`.

## Usage 
Add `"jade-brunch": "x.y.z"` and `"static-jade-brunch": "x.y.z"` to `package.json` of your brunch app.

*Pick a plugin version that corresponds to your minor (y) brunch version.*

If you want to use git version of plugin, add:

* `"jade-brunch": "git+ssh://git@github.com:brunch/jade-brunch.git"`
* `"static-jade-brunch": "git+ssh://git@github.com:ilkosta/static-jade-brunch.git"`


### Useful convensions
Brunch concatenates all your files in `app/`, `test/` and `vendor/` directories to two files by default:

* `app.js` contains your application code.
* `vendor.js` contains code of libraries you depend on (e.g. jQuery).

To avoid the inclusion of compiled jade file in `app.js` by the `jade-brunch` plugin, is possible to add a `template` file handler that point to a different output file. Inside config.coffee:
```coffeescript
templates:
      joinTo:
        'js/templates.js': /.+\.jade$/
```

The `brunch` compiler **ignore** each file starting with `_` (underscore) and that is useful for the chunks of jade that are included or extended.

The `brunch` compiler **copy** the content of the `assets/` directory without recompile it. 
To permit others plugin (eg. auto-reload-brunch plugin) to *manage* the files generated by `static-jade-brunch`, all the generated files are placed inside the `assets/` directory.

If before the brunch compilation the directory structure is something like:
```
app
| assets
| | font
| | img
| scripts
| styles
| partials
| | presentation.jade
| index.jade	
```
after the `brunch build` the content of app directory would be like:
```
| assets
| | font
| | img
| | partials
| | | presentation.html
| | index.html
| scripts
| styles
| partials
| | presentation.jade
| index.jade
```
and the content of the `public/` directory:
```
css
| ...
js
| app.js
| templates.js
| vendor.js
partials
| presentatin.html
index.html
```


## License
Copyright (c) 2012 "ilkosta" Costantino Giuliodori.

Licensed under the [MIT license](https://github.com/ilkosta/static-jade-brunch/blob/master/LICENSE-MIT).