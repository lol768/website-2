# [Flutter][]'s website

The website for [Flutter][].

[![Build Status](https://travis-ci.org/flutter/website.svg?branch=master)](https://travis-ci.org/flutter/website)

## Issues, bugs, and requests

We welcome contributions and feedback on our website!
Please file a request in our
[issue tracker](https://github.com/flutter/flutter/issues/new)
and we'll take a look.

## Developing

Install Jekyll and related tools by following the
[instructions](https://help.github.com/articles/using-jekyll-with-pages/)
provided by GitHub.

A tldr version follows:

1. Ensure you have [Ruby](https://www.ruby-lang.org/en/documentation/installation/) installed; you need version 2.2.2 or later:<br>
`ruby --version`

1. Ensure you have [Bundler](http://bundler.io/) installed; if not install with:<br>
`gem install bundler`

1. Install all dependencies:<br>
`bundle install`

1. Create a branch.

1. Make your changes.

1. Test your changes by serving the site locally:<br>
`bundle exec jekyll serve` (or `jekyll serve -w --force_polling`)

1. Prior to submitting, run link validation:<br>
`rake checklinks`

## Writing for flutter.io

(Eventually, this section should be expanded to its own page.)

### Adding next/previous page links

If you have a document that spans multiple pages, you can add next and previous
page links to make navigating these pages easier. It involves adding some information
to the front matter of each page, and including some HTML.

```
---
layout: tutorial
title: "Constraints"

permalink: /tutorials/layout/constraints.html
prev-page: /tutorials/layout/properties.html
prev-page-title: "Container Properties"
next-page: /tutorials/layout/create.html
next-page-title: "Create a Layout"
---

{% include prev-next-nav.html %}

{:toc}

<!-- PAGE CONTENT -->

{% include prev-next-nav.html %}
```

Omit the "prev-page" info for the first page, and the "next-page" info for the
last page.

## Syntax highlighting

The flutter.io website uses [prism.js](http://prismjs.com/) for syntax
highlighting. This section covers how to use syntax highlighting, and
how to update our syntax highlighter for new languages.

### Supported languages

This website can syntax highlight the following languages:

* shell
* dart
* html
* css
* javascript
* java
* objectivec
* swift

### Using syntax highlighting

The easiest way to syntax highlight a block of code is to wrap
it with triple backticks followed by the language.

Here's an example:

<!-- skip -->

	```dart
	class SomeCode {
	  String name;
	}
	```


See the list of supported languages above for what to use
following the first triple backticks.

### Adding more languages for syntax highlighting

The flutter.io website uses a custom build of prism, which
includes only the languages the website requires. To improve
load times and user experience, we do not support every
language that prism supports.

To add a new language for syntax highlighting, you will need
to generate a new copy of the `prism.js` file.

Follow these steps to generate a new copy of `prism.js`:

* Open `js/prism.js`
* Copy the URL in the comment of the first line of the file
* Paste it into a browser window/tab
* Add the new language that you wish to syntax highlight
* DO NOT change the other plugins, languages, or settings
* Download the generated JavaScript, and use it to replace `js/prism.js`
* Download the generated CSS, and use it to replace `_sass/_prism.scss`

## Advanced stylization of code blocks

Do you want to highlight (make the background yellow)
code inside a code block? Do you want to strike-through
code inside a code block? We got that!

For syntax highlighting, plus yellow highlighting
and strike-through formatting, use the `prettify` tag
with additional custom inline markup.

If you want to highlight a specific bit of code, use the
`[[highlight]]highlight this text[[/highlight]]` syntax
with the `prettify` tag.

For example:

<!-- skip -->
{% prettify dart %}
void main() {
  print([[highlight]]'Hello World'[[/highlight]]);
}
{% endprettify %}

If you want to strike-through a specific bit of code, use the
`[[strike]]highlight this text[[/strike]]` syntax
with the `prettify` tag.

For example:

<!-- skip -->
{% prettify dart %}
void main() {
  print([[strike]]'Hello World'[[/strike]]);
}
{% endprettify %}

The `prettify` plugin will also unindent your code.

If you want to see how this functionality was added to this site, refer to
[this commit](https://github.com/flutter/website/commit/ea15f52fe47d3a7b6313ac58d07c66f3b29fe74d).

## Including a region of a file

You can include a specific range of lines from a file:

```ruby
{% include includelines filename=PATH start=INT count=INT %}
```

`PATH` must be inside of `_include`. If you are including source code,
place that code into `_include/_code` to follow our convention.

## Code snippet validation

The code snippets in the markdown documentation are validated as part of the
build process. Anything within a '\`\`\`dart' code fence will be extracted into
its own file and checked for analysis issues. Some ways to tweak that:

- If a code snippet should not be analyzed, immediately proceed it with
  a `<!-- skip -->` comment
- To include code to be analyzed, but not displayed, add that in a comment
  immediately proceeding the snippet (e.g., `<!-- someCodeHere(); -->`)
- A snippet without any import statements will have an import
  (`'package:flutter/material.dart'`)
  automatically added to it
- We ignore special formatting tags like `[[highlight]]`.

[Flutter]: https://flutter.io
