# hugo-best-practices

Best practices and ideas for [Hugo](https://gohugo.io/) the open-source static site generator.

## Copy the theme folder content

x

## CSS and JavaScript

Old themes kept the css and js files in the static folder. Sometimes tools like Gulp, Grunt and Webpack were used for pre-processing.
The latest version of Hugo will do all the stuff like bundling and minifiy for you. For this to work the files have to be put in the `assets` folder.

There are three critical methods to use as the bare minimum `minify`, `fingerprint` and `slice`. SCSS might make use of `toCSS` and `postCSS`.

With `minify` you will get a minified version of your files.

The `fingerprint` adds a unique string to the name so that the browser won't cache your files on modification.

Finally `slice` allows you to concat multiple files to a new one. This works best with `minify`.

### CSS

Putting the above methods in place the minified `main.css` will be created as described below. Keep in mind that the files has to be in the `assets` folder.

```html
{{ $stylemain := resources.Get "css/main.css" | minify | fingerprint }}
<link rel="stylesheet" href="{{ $stylemain.Permalink }}" integrity="{{ $stylemain.Data.Integrity }}">
```

### Javascript

Usually a theme will contain multiple JS files which might require a specific order. This is where `slice` comes into handy.

```html
{{ $jquery := resources.Get "/js/jquery-v6.6.6/jquery.min.js" }}
{{ $bootstrap := resources.Get "/js/bootstrap-v4.2.0/bootstrap.min.js" }}
{{ $main := resources.Get "/js/main.js" }}

{{ $fullscript := slice $jquery $bootstrap $main | resources.Concat "/js/vendor.js" | minify | fingerprint }}
<script src="{{ $fullscript.Permalink }}"></script>
```

## Images

x

## Front-End Checklist

Walk trough every point in the [Front-End Checklist](https://github.com/thedaviddias/Front-End-Checklist)
