# Nova Mod: Parser Events

This mod adds the ability to listen for parser events, namely the `parse_string` method used to generate Nova emails.

## Requirements

This extension requires:

- Nova 2.6+

## Installation

If you do not already have a file `application/libraries/MY_Parser.php`, simply copy the file `application/libraries/MY_Parser.php` into your `application/libraries` folder.

If you do have a custom file `application/libraries/MY_Parser.php` already, you need to copy the `parse_string` method from the corresponding module in this file into your existing file. If you already have a custom version of `parse_string` not from this mod, then you'll need to modify your code to emit the two events as shown in this module's file.

## Usage

This mod adds two events:

1. `parser.parse_string.data.[route...]`, where the route segments from your URL are separated by `.`; and
1. `parser.parse_string.output.[route...]`, where the route segments from your URL are separated by `.`.

The `parser.parse_string.data` is emitted before the string is parsed, allowing you to manipulate the data being loaded into the string (contained in the property `data` in the event object passed to the listener). The `parser.parse_string.output` is emitted after the string has been parsed, allowing you to manipulate the output of the parser (contained in the property `output` of the event object passed to the listener).

An example of manipulating the data for the emails sent from the join form:

```
$this->event->listen(['parser', 'parse_string', 'data', 'main', 'join'], function($event){
    // edit properties of $event['data']
});
```

An example of manipulating the output of the emails sent from the join form:

```
$this->event->listen(['parser', 'parse_string', 'output', 'main', 'join'], function($event){
    // edit the string $event['output']
});
```

## Issues

If you encounter a bug or have a feature request, please report it on GitHub in the issue tracker here: https://github.com/jonmatterson/nova-mod-parser_events/issues

## License

Copyright (c) 2019 Jon Matterson.

This module is open-source software licensed under the **MIT License**. The full text of the license may be found in the `LICENSE` file.
