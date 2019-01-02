# spring-test-viewspec
Simplifies testing of Spring MVC views

## Rationale
Unit testing a Spring MVC View can lead to lots of boilerplate code:

```
mockMvc.perform(get(StartController.START))
  .andExpect(status().isOk())
  .andExpect(content().contentType("text/html;charset=UTF-8"))
  .andExpect(view().name("start"))
  .andExpect(xpath("//h1").string("Start"));
...
```
and this is before we even start on testing input fields, and errors.

The problem with this approach is that what is actually being tested gets lost in the code.
It's easy to get snow-blind and make mistakes:

* Maintain a consistent approach across all views
* Forget to test standard elements
* Forget to test new view elements, such as fields

## Requirements
General requirements capture of a library. Feel free to contibute

### Simple API
A simple way to verify standardised views in Spring MVC tests:

Can check conformance to multiple 'features' in one line
* Allow configuration of features, e.g. ID 'convention'
* Fluent API (or autoconfigure)
* Exclusions to 'specification' must be explicitly made

### Extend MockMvc
Where MockMvc is deficient, improve it:

* Ability to AND/OR ResultMatchers
* More sophisticated use of xpath - e.g. able to make assertions against NodeList

### Conformant XHTML
Feature to check XHTML is well formed, valid and obeys standard 'good practice':

* Only one <h1> within a <section> or entire document if not sectioned
* Unique IDs
* IDs follow naming convention
* Safe charset - no use of copy pasted Word apostrophes or pound signs

### Fields
* <input> associated with <label>
* <input> in error has associated error markup

### Accessibility
Might be too much to handle initially:

* W3C checks - can we find a java library 
