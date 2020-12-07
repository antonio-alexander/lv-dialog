# lv-dialog

lv-dialog is a library that attempts to provide alternatives for the handful of basic ways to communicate with the user. In lieu of the built-in dialog VIs, this library provides a semi-static api and class based backend that will allow you to provide your own dialogs.

If any of the following is true (or desired) this library could solve your problem:

* A desire to have dialogs that match your user interface
* A desire to be able to communicate with the user and standardize how its integrated into your application
* Are REALLY interested in seeing how you can re-size a window with controls.
* Have a user interface/wizard flow that requires multiple inputs from a user, but not all at once
* Have a desire to centralize all of the dialogs for a given application

There are two libraries included: lv-dialog.lvlib and lv-dialog-interfaces.lvlib, although they are provided together, lv-dialog-interfaces depends on lv-dialog and not the opposite. lv-dialog-interfaces can be used as a template to create your own libraries.

## lv-dialog-interfaces

lv-dialog-interfaces is an implementation of lv-dialog, it inherits from the class in lv-dialog and implements all of the interfaces.  There's nothing really spectacular about the implementation other than the following (in my opinion):

* Most of the dialogs can automatically re-size depending on the text provided
* The dialog boxes will automatically go to the monitor that contains the vi reference it was called (or referenced) from

## Forward Compatibility

The lv-dialog library's api is setup such that the api is namespaced by its major version (v1), although i don't expect there to be any changes in the long-term of this package that would require modifying the major version, in the event that it does, there will be a new API and the older version will remain.

## Examples

There are a handful of examples, see lv-dialog.lvlib:api/v1/examples.

## Utilities

There are only a couple of utilities VIs, unfortunately (or obviously), they are not pure LabVIEW, but can help or serve as alternatives to (wait for it) built-in VIs.

### Error Handler (error_handler&#46;vi)

The error handler implements the error handling similar to the "Simple Error Handler&#46;vi" but will call the loaded instance of the error_window when displaying an error.

This VI will automatically call the loaded instance using a functional global, be careful that this functional global or the get_class VI remains in-memory if calling within a VI running asynchronously.

### Feedback (feedback&#46;vi)

Feedback is a polymorphic VI that can be used to indicate feedback when an error occurs (negative), when an error doesn't occur (positive) or both (postive/negative). It does this using a combination of the error_window, one_button and two_button dialogs.

This VI will automatically call the loaded instance using a functional global, be careful that this functional global or the get_class VI remains in-memory if calling within a VI running asynchronously.

### File Dialog (file&#46;vi)

This provides the same functionality as the built-in file dialog, but does so using .NET.

Although the input VI isn't used, it's future goal is to allow the window to be loaded on the same monitor as the VI reference wired in.

### Folder Dialog (folder&#46;vi)

This is identical to the file&#46;vi using folders or the built-in file dialog, but does so for a folder using .NET. This may be more aesthetically pleasing or more obvious that you need to pick a folder and NOT a file.

Although the input VI isn't used, it's future goal is to allow the window to be loaded on the same monitor as the VI reference wired in.

## API

The api is implemented using classes that override the base class, it can be done by using the load_class&#46;vi, which will store it in a private functional global to be accessed by the utilities. Also, some of the utilities will access those VIs using a conditional disable diagram tied to the major version ("lv_dialog_api_version") which is defaulted to 1. Otherwise you're forced to pass the class around in your code for integration.

## API (v1)

The api is implemented as a class owned by lv-dialog.lvlib:/api/v1/public/class/v1.lvlib, the class can be used to implement your own, or use the ni based express VIs wrapped in the api, for api that have no built-in equivalent, it will output the not implemented error.

### One Button (one_button&#46;vi)

This approximates the functionality of the built-in one button dialog; the api has inputs for the message it displays and the text on the button. On return it will indicate the interaction with the interface. In general, it should only be button_1 or panel_closed, but depending on the implementation other items can be used.

This IS implemented by the base api class using the built-in one button dialog.

### Two Button (two_button&#46;vi)

This approximates the functionality of the built-in two button dialog; the api has inputs for the message it displays and the text on each of the two buttons. On return it will indicate the interaction with the dialog (generally button_1, button_2 or panel_closed).

This IS implemented by the base api class using the built-in two button dialog.

### Three Button (three_button&#46;vi)

This approximates the functionality of the built-in three button dialog; the api has inputs for the message it displays and the text on each of the three buttons. On return it will indicate the interaction with the dialog (generally button_1, button_2, button_3 or panel_closed).

This IS implemented by the base api class using the built-in three button dialog.

### Combo Box Input (combo_box_input&#46;vi)

This approximates the "Prompt User for Input" Express VI, but in an opinionated way. The configuration allows you to provide the text on two buttons, the strings to use to populate the combo box as well as whether or not a custom string is allowed. On return it will indicate the interaction with the dialog (generally button_1, button_2 or panel_closed) as well as the output string.

If using this dialog with an enum, use the []Strings property node of an enum control and the format to string function to convert it back into an enum.

This is NOT implemented by the base api class.

### Data Entry Numeric (data_entry_numeric&#46;vi)

This approximates the "Prompt User for Input" Express VI, but in an opinionated way. The configuration allows you to provide text on two buttons as well as the dialog box. On return it will indicate the interaction with the dialog (generally button_1, button_2 or panel_closed) as well as the output double.

This is NOT implemented by the base api class.

### Data Entry String (data_entry_string&#46;vi)

This approximates the "Prompt User for Input" Express VI, but in an opinionated way. The configuration allows you to provide the text on two buttons as well as the string indicator. On return it will indicate the interaction with the dialog (generally button_1, button_2 or panel_closed) as well as the output string.

This is NOT implemented by the base api class.

### Confirmation Input (confirm_input&#46;vi)

The confirmation input is a unique implementation of the two button dialog, it's meant to be used to have the user "affirm" something by first typing in text which enables the button. that they can then press. This is meant to be a dialog to wrap "dangeous" operations.

This is NOT implemented by the base api class.

### Busy Wait (busy_wait&#46;vi) or Busy Wait Embedded (busy_wait_embed&#46;vi)

The busy/wait api can be used to provide feedback when a process is going to take a long time, as implemented within the base api class, it doesn't have a lot of functional feedback aside from setting or unsetting busy. The configuration provides a time (in seconds), the dialog message as well as an event registration that can be used to indicate "done" from the outside.

This is implemented by the base api class (not the embedded) by using the "Set Busy" and "Unset Busy" VIs.

### Error Window (error_window&#46;vi)

The error window is meant to approximate the simple error handler. The implementation is kind of jank/garbage, but it's functional.

This IS implemented by the base api class using the "General Error Handler&#46;vi"
