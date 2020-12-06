# lv-dialog

lv-dialog is a library that attempts to provide alternatives for the handful of basic ways to communicate with the user. In lieu of the built-in dialog VIs, this library provides a semi-static api and class based backend that will allow you to provide your own dialogs.

If any of the following is true (or desired) this library could solve your problem:

* A desire to have dialogs that match your user interface
* A desire to be able to communicate with the user and standardize how its integrated into your application
* Are REALLY interested in seeing how you can re-size a window with controls.
* Have a user interface/wizard flow that requires multiple inputs from a user, but not all at once
* Have a desire to centralize all of the dialogs for a given application

There are two libraries included: lv-dialog.lvlib and lv-dialog-interfaces.lvlib, although they are provided together, lv-dialog-interfaces depends on lv-dialog and not the opposite. lv-dialog-interfaces can be used as a template to create your own libraries.

## Forward Compatibility

The lv-dialog library's api is setup such that the api is namespaced by its major version (v1), although i don't expect there to be any changes in the long-term of this package that would require modifying the major version, in the event that it does, there will be a new API and the older version will remain.

## Examples

There are a handful of examples, see lv-dialog.lvlib:api/v1/examples.

## Utilities

## API

The api is implemented as a class owned by lv-dialog.lvlib:/api/v1/public/class/v1.lvlib, the class can be used to implement your own, or use the ni based express VIs wrapped in the api, for api that have no built-in equivalent, it will output the not implemented error.

### One Button (one_button.vi)

### Two Button (two_button.vi)

### Three Button (three_button.vi)

### Combo Box Input (combo_box_input.vi)

### Confirmation Input (confirm_input.vi)

### Data Entry Numeric (data_entry_numeric.vi)

### Data Entry String (data_entry_string.vi)

### Busy Wait (busy_wait.vi) or Busy Wait Embedded (busy_wait_embed.vi)

### Error Window (error_window.vi)

## lv-dialog-interfaces

lv-dialog-interfaces is an implementation of lv-dialog, it inherits from the class in lv-dialog and implements all of the interfaces.  There's nothing really spectacular about the implementation other than the following (in my opinion):

* Most of the dialogs can automatically re-size depending on the text provided
* The dialog boxes will automatically go to the monitor that contains the vi reference it was called (or referenced) from
