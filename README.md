AutoCompleter (v1.1)
====================

Credit: Harald Kirschner - http://digitarald.de/project/autocompleter/

This AutoCompleter script for [MooTools](http://mootools.net/) provides the functionality for text suggestion and completion. 
It features different data-sources (local, JSON or XML), a variety of user interactions, custom formatting, multiple selection, 
animations and much more.


Showcases
---------

See Docs folder of project

* Local Tag - Autocompleted tags in input fields and textareas, controlled by keyboard and mouse.
* Local - Countries Token array is filtered on client-side, not requested from the server.
* HTML Request
* JSON Request


Features
--------

* Use local data or Ajax request (JSON or XHTML) as data source.
* Look and feel like the OS, visitors can use it without problems.
* Intuitive navigation with mouse and keyboard.
* Customizable behaviour with a lot of options and events.
* Minimal effects to avoid noise in the workflow.

How to use
----------

### With JSON + PHP5/PDO

      window.addEvent('domready', function() {
 
          new Autocompleter.Request.JSON('fe-searchuser', '/query_user.php', {
              'postVar': 'search'
          });
 
      });
      
Your XHTML markup, no additional elements needed:

      <input type="text" name="search" id="fe-search"/>
      
And the example PHP for the database query:

      <?php
      // query_user.php
 
      $search = $_POST['search'];
      $result = array();
 
      // Some simple validation
      if (is_string($search) && strlen($search) > 2 && strlen($search) < 64)
      {
          $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
 
          // Building the query
          $stmt = $dbh->prepare("SELECT name FROM users WHERE name LIKE ?");
 
          // The % as wildcard
          if ($stmt->execute(array($search . '%') ) )
          {
              // Filling the results with usernames
              while (($row = $stmt->fetch() ) )
              {
                  $result[] = $row['name'];
              }
          }
      }
 
      // Finally the JSON, including the correct content-type
      header('Content-type: application/json');
 
      echo json_encode($result); // see NOTE!
 
      ?>
      
*NOTE*: (If you are scared of the PHP 5 example) PHP 5 is not needed, this is just an example! There are classes and native solutions for all languages, 
more information is available here: [JSON.org](http://json.org/) (List at the bottom of the page)

The response for a "Har" search would look like:

      ["Harald","Haribald","Harold","Harry","Haribald"]


Documentation
-------------

[Aaron Newton](http://www.mootorial.com/) wrote some documentation for CNET Clientside, describing the Options, Events and some public methods:

External [Autocompleter Documentation](http://clientside.cnet.com/docs/3rdParty/Autocompleter) - NOTE: This site is no longer available


Requirements
------------

### MooTools JavaScript Framework

Download [MooTools 1.4.5 Core](http://mootools.net/core) with at least these modules:

* Element.Dimensions
* Fx.Tween
* Request.HTML (for HTML requests)
* Request.JSON (for JSON requests)
* DomReady (facultative)
* Selectors (facultative)


Changelog
---------

### 1.1.3 (2012-05-16)
* Working with MooTools 1.4.5
* Fixed: Problem with null strings
* Added: spinner.gif for progress indicator to main styles

### 1.1.2 (2008-08-19)
* Added: Option indicator for Autocompleter.Ajax, element is shown during request.
* Added: Option indicatorClass, class-name is added during request to input.
* Added: Option visibleChoices (default true), to scroll hidden choices into view
* Added: Option emptyChoices, called instead of hideChoices when tokens are empty.
* Fixed: Fixed filter loops on RegExp::test for Opera.
* Fixed: Element::getSelectedRange returns correct positions for textareas in IE.
* Fixed: Selected item resets correctly.
* Fixed: Update can now also handle tokens as Hash, length check fixed.
* Changed: BREAKING CHANGE (incl. Compatibility)! Naming conventions following MooTools 1.2
 * Autocompleter.Base to Autocompleter
 * Autocompleter.Ajax to Autocompleter.Request
 * Autocompleter.Ajax.Json/Xhtml to Autocompleter.Request.JSON/HTML
* Changed: BREAKING CHANGE (incl. Compatibility)! Extracted Local and Request from Autocompleter.js
* Changed: Removed Element::getOffsetParent, included in MooTools 1.2
* Changed: Element::getCaretPosition renamed to Element::getSelectedRange
* Changed: Added JSON and HTML Request showcases.

### 1.1.1 (2008-04-27)
* Fixed: Removed orphaned trash events and added destroy for fix overlay.
* Fixed: Added missing addChoiceEvents call to default injectChoice in Autocompleter.Ajax.Xhtml to add mouse events.

### 1.1 (2008-03-28)
* Added: Support for tagging, multiple entries with configurable parsers (allowing commas, spaces …)
* Added: Option selectMode for different select behaviours
* Added: Option overflow for scrolling through more suggestions
* Added: Options filter, filterCase and filterSubset, for easier locale usage, better query marks and to prepare caching feature
* Added: Option autoSubmit to automatically submit the form on enter.
* Added: Option forceSelect to allow select-box behaviour
* Added: Option typeAhead for fast and simple suggestions (works best with forceSelect)
* Changed: Updated to MooTools 1.2 dev
* Changed: New Events for a better widget control
* Fixed: Selection behaviour works a lot better, also for tagging
* … and more fixes

### 1.0.4 (2007-05-23)
* Fixed: Fix for & that has the Event::code of key-up (only for keypress event)
* Changed: Added overflown option to the options object and more clean-up’s

### 1.0.3 (2007-05-20)
* Official release with support for local, JSON and HTML responses


License
-------

All files are © 2008-2009 by Harald Kirschner and available under the [MIT License](http://www.opensource.org/licenses/mit-license.php).


Contact & Discussion
--------------------

For asking questions, requesting features, filing bugs or contributing other thoughts on this project use the [support forum](http://digitarald.de/forums/) below. 
Before posting a new question, read through the documentation and the contributed notes for an answer. For problem reports make sure to add enough details like 
browser, version and a link or the relevant code.
