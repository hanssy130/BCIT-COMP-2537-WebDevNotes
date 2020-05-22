# Week 2 — JQuery / NodeJS

## JQuery
```
$(document).ready(function() {
  // jQuery method
});
```
Executes when the DOM is ready

`$('tagName')`
`$('#identifier')`
`$('.className')`

### Events
- click
- mouseover
- document ready - when page loads

`$('#button').on('click', function() {/* do something */ })`

### DOM Manipulation
- Get
`let content = $('#para').html()`

- Set
`$('#para').html('Some <b>new</b> content')`

- Remove
`remove()`

- Append
`$('New content.').appendTo('p')`

- Prepend
`$('New content.').appendTo('p')`

- Before
```$('p').before('<p>New content.</p>)

or

$('<p>New content</p>').insertBefore('p')```
