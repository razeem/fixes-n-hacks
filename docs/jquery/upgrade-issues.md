# jQuery 3 Upgrade Issues

## jQuery 3 Upgrade Issues
- Error with owl carousel: `TypeError: $(...).find(...).andSelf is not a function`
- Fix:
```js
$.fn.andSelf = function () {
  return this.addBack.apply(this, arguments);
}
```
- Bootstrap's JavaScript requires jQuery 1.9.1 or higher, but lower than 3. Use bootstrap v3.3.7.

## Custom Validation Example
```js
function customValidateForm(inputForm) {
  // ...existing code...
}
customValidateForm('webform-submission-kids-library-call-me-back-form');
```

## Week Picker
- See: https://github.com/Prezent/jquery-weekpicker
- Example: http://jsfiddle.net/manishma/AVZJh/light/
