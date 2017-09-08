---
title: Cypress.Commands.overwrite
comments: false
---

Cypress comes with its own API for creating custom commands and even overwriting existing commands. In fact, the same public methods *you* have access to from our API is used to build every command in our API.

{% note info  %}
A great place to define or overwrite commands is in your `cypress/support/commands.js` file, since it is loaded before any test files are evaluated.
{% endnote %}

# Syntax

```javascript
Cypress.Commands.overwrite(name, callbackFn)
Cypress.Commands.overwrite(name, options, callbackFn)
```

## Usage

**{% fa fa-check-circle green %} Correct Usage**

```javascript
Cypress.Commands.overwrite('visit', (orig, url, options) => {})
```

## Arguments

**{% fa fa-angle-right %} name** ***(string)***

Name of command to overwrite.

**{% fa fa-angle-right %} callbackFn** ***(Function)***

Pass a function that takes the arguments passed to the command.

**{% fa fa-angle-right %} options** ***(Object)***

Pass in an options object to change the behavior of the command.

Option | Default | Description
--- | --- | ---
`prevSubject` | `false` | how to handle the previously yielded subject.

The `prevSubject` accepts the following values:

- `true`: use the subject yielded from the previously chained command. (parent command)
- `false`: ignore any existing subject from previously chained command. (child command)
- `dom`: use the subject yielded from the previously chained command. Expects subject to be a DOM element. (child command)
- `optional`: may or may not have an existing subject (dual command)

# Examples

## Overwrite Existing Command

You can modify the logic of existing Cypress commands or previously defined custom commands.

```javascript
Cypress.Commands.overwrite('visit', function(orig, url, options){
  // modify url or options here...
  return orig(url, options)
})
```

# See also

- {% url 'Cypress.Commands.add' add %}
