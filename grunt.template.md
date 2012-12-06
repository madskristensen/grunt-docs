Template strings can be processed manually using the provided template functions. In addition, the config.get method (used by many tasks) automatically expands `<% %>` style template strings specified as config data inside the Gruntfile.

### grunt.template.process
Process a [Lo-Dash template](http://lodash.com/docs/#template) string. The `template` argument will be processed recursively until there are no more templates to process.

The default data object is the entire config object, but if `options.data` is set, that object will be used instead. The default template delimiters are `<% %>` but if `options.delimiters` is set to a valid delimiter name, those template delimiters will be used instead.

_See the `grunt.template.setDelimiters` method for a list of valid delimiter names._

```js
grunt.template.process(template [, options])
```

Inside templates, the `grunt` object is exposed so that you can do things like `<%= grunt.template.today('yyyy') %>`. _Note that if the data object already has a `grunt` property, the `grunt` API will not be accessible in templates._

In this example, the `baz` property is processed recursively until there are no more `<% %>` templates to process.

```js
var obj = {
  foo: 'c',
  bar: 'b<%= foo %>d',
  baz: 'a<%= bar %>e'
};
grunt.template.process('<%= baz %>', {data: obj}) // 'abcde'
```

### grunt.template.setDelimiters
Set the [Lo-Dash template](http://lodash.com/docs/#template) delimiters to a predefined set in case you `grunt.util._.template` needs to be called manually.

_You probably won't need to use this method, because you'll be using `grunt.template.process` which uses this method internally._

Valid names:

* `config` - use `<% %>` style delimiters (default)
* `init` - use `{% %}` style delimiters (used in [init task](task_init.md) templates)
* `user` - use `[% %]` style delimiters (not used internally in grunt)

```js
grunt.template.setDelimiters(name)
```

### grunt.template.addDelimiters
Add a named set of [Lo-Dash template](http://lodash.com/docs/#template) delimiters. A few sets have already been added for your convenience, see the `grunt.template.setDelimiters` method for a list.

_You probably won't need to use this method, because the built-in delimiters should be sufficient._

```js
grunt.template.addDelimiters(name, opener, closer)
```

## Helpers

### grunt.template.date
Format a date using the [dateformat library](https://github.com/felixge/node-dateformat).

```js
grunt.template.date(date, format)
```

In this example, a specific date is formatted as month/day/year.

```js
grunt.template.date(847602000000, 'yyyy-mm-dd') // '1996-11-10'
```

### grunt.template.today
Format today's date using the [dateformat library](https://github.com/felixge/node-dateformat).

```js
grunt.template.today(format)
```

In this example, today's date is formatted as a 4-digit year.

```js
grunt.template.today('yyyy') // '2012'
```

_(somebody remind me to update this date every year so the docs appear current)_