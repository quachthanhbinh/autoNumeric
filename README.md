## What is [autoNumeric](http://www.decorplanit.com/plugin/)?

autoNumeric is a library that provides live *as-you-type* formatting for international numbers and currencies.

#### Highlights
autoNumeric main features are :
- Easy to use and configure
```javascript
// Initialization
$('.myInput').autoNumeric('init', { currencySymbol : '$' });
```
- Very high configurability (more than 30 [options](#options) available)
```javascript
// The options are...optional :)
const autoNumericOptionsEuro = {
    digitGroupSeparator        : '.',
    decimalCharacter           : ',',
    decimalCharacterAlternative: '.',
    currencySymbol             : ' €',
    currencySymbolPlacement    : 's',
    roundingMethod             : 'U',
};

// Initialization
$('.myInput').autoNumeric('init', autoNumericOptionsEuro);
```
- User experience oriented ; using autoNumeric just feels right and natural
- Supports most international numeric formats and currencies<br>*(If the one you use is not supported yet, open an [issue](https://github.com/BobKnothe/autoNumeric/issues/new) and we'll add it as soon as possible!)*

*And also:*
- Any number of different formats can be used at the same time on the same page.<br>Each input can be configured by either setting the options as HTML5 data attributes, or directly passed as an argument in the Javascript code
- The settings can easily be changed at *any* time using the `update` method or via a callback
- autoNumeric supports most text elements, allowing you to place formatted numbers and currency on just about any part of the page
- 18 built-in [methods](#methods) gives you the flexibility needed to use autoNumeric to its maximum potential
- More than 30 [options](#options) allows you to customize the output format

With that said, autoNumeric supports most International numeric formats and currencies including those used in Europe, Asia, and North and South America.

****

## Getting started

### How to use?
Simply include jQuery and autoNumeric (in that order) in your html header tag.<br>No other file or library are required.

```html
<script src="jquery.js" type="text/javascript"></script>
<script src="autoNumeric.js" type="text/javascript"></script>
```

Initialize autoNumeric and pass any options :

```javascript
$(document).ready(function() {
   $(selector).autoNumeric('init'); //autoNumeric with defaults
});

$(document).ready(function() {
   $(selector).autoNumeric('init', { options }); //autoNumeric with options being passed
});
```

You're done!

### On which elements can it be used?
Here are the following supported input types:
- `text`,
- `tel`,
- `hidden`, or
- no type specified at all

```html
<input type='text' value="1234.56">
<input type='tel' value="1234.56">
<input type='hidden' value="1234.56">
<input value="1234.56">
```

Note : the `number` type is **not** supported simply because autoNumeric formats numbers as strings (ie. `'123.456.789,00 &#8364;'`) that this input type does not allow.

## Options
Multiple options allow you to customize precisely how a form input will format your inputs as you type :

| Option           | Description | Default Value |
| :---------------- | :-----------:  | :-----------:  |
| `digitGroupSeparator` | Thousand separator character  | `','` |
| `noSeparatorOnFocus` | Remove the thousand separator, currency symbol and suffix on focus | `false` |
| `digitalGroupSpacing` | Digital grouping for the thousand separator | `'3'` |
| `decimalCharacter` | Decimal separator character | `'.'` |
| `decimalCharacterAlternative` | Allow to declare alternative decimal separator which is automatically replaced by the *real* decimal character (useful in countries where the keyboard numeric pad have a period as the decimal character) | `null` |
| `currencySymbol` | Currency symbol | `''` |
| `currencySymbolPlacement` | Placement of the currency sign, relative to the number (as a prefix or a suffix) | `'p'` |
| `negativePositiveSignPlacement` | Placement of negative/positive sign relative to the currency symbol (possible options are `l` (left), `r` (right), `p` (prefix) and `s` (suffix)) | `null` |
| `suffixText` | Additional text suffix that is added after the number | `''` |
| `overrideMinMaxLimits` | Override minimum and maximum limits (possible options are `ceiling`, `floor` and `ignore`) | `null` |
| `maximumValue` | Maximum possible value | `'9999999999999.99'` |
| `minimumValue` | Minimum possible value | `'-9999999999999.99'` |
| `decimalPlacesOverride` | Maximum number of decimal places (used to override decimal places set by the minimumValue & maximumValue values) | `null` |
| `decimalPlacesShownOnFocus`| Expanded decimal places visible when input has focus | `null` |
| `scaleDivisor`| This option decides the onfocus value and places the result in the input on focusout | `null` |
| `scaleDecimalPlaces`| The number of decimal places when unfocused | `null` |
| `scaleSymbol`| Symbol placed as a suffix when unfocused | `null` |
| `saveValueToSessionStorage`| Allow the `decimalPlacesShownOnFocus` value to be saved into session storage | `false` |
| `onInvalidPaste`| Manage how autoNumeric react when the user tries to paste an invalid number (possible options are `error`, `ignore`, `clamp`, `truncate` or `replace`) | `'error'` |
| `roundingMethod`| Method used for rounding (possible options are `S`, `A`, `s`, `a`, `B`, `U`, `D`, `C`, `F`, `N05`, `U05` or `D05`) | `'S'` |
| `allowDecimalPadding`| Allow padding the decimal places with zeros | `true` |
| `negativeBracketsTypeOnBlur`| Adds brackets `[]`, parenthesis `()`, curly braces `{}` or `<>` on negative values when unfocused | `null` |
| `emptyInputBehavior`| Define what to display when the input value is empty (possible options are `focus`, `press`, `always` and `zero`) | `'focus'` |
| `leadingZero`| Controls the leading zero behavior (possible options are `allow`, `deny` and `keep`) | `'deny'` |
| `formatOnPageLoad`| Determine if the default value will be formatted on initialization | `true` |
| `selectNumberOnly`| Determine if the select all keyboard command will select the complete input text, or only the input numeric value | `false` |
| `defaultValueOverride`| Helper option for the ASP.NET-specific postback issue | `null` |
| `unformatOnSubmit`| Removes formatting on submit event | `false` |
| `outputFormat`| Defines the localized output format of the `get`, `getString` & `getArray` methods | `null` |
| `showWarnings`| Defines if warnings should be shown | `true` |
| `failOnUnknownOption `| This option is the 'strict mode' (aka 'debug' mode), which allows autoNumeric to strictly analyse the options passed, and fails if an unknown options is used in the settings object. | `false` |

For more detail on how to use each options, please take a look at the detailled comments in the source code for the `defaultSettings` object.

## Methods
autoNumeric provides numerous methods to access and modify the input value, formatted or unformatted, at any point in time.
<br>It does so by either providing access to those methods via the jQuery wrapper, or directly from the autoNumeric ES6 module.

#### jQuery plugin calls
| Method           | Description | Call example |
| :---------------- | :-----------:  | :-----------:  |
| `init` | Initialize autoNumeric and attach the settings (options can be passed as a parameter). **This must be run before other methods can be called.**  | `$(someSelector).autoNumeric('init', {options});` |
| `destroy` | Stop and remove autoNumeric for the current element | `$(someSelector).autoNumeric("destroy");` |
| `wipe` | Clear the value from sessionStorage (or cookie, depending on browser supports) | `$(someSelector).autoNumeric("wipe");` |
| `update` | Updates the autoNumeric settings, which reformat the input on-the-fly | `$(someSelector).autoNumeric("update", {options});` |
| `set` | Set the value given as a parameter, and formats it | `$(someSelector).autoNumeric('set', '12345.67');` |
| `unSet` | Unformat inputs (handy right before form submission) | `$(someSelector).autoNumeric('unSet');` |
| `reSet` | Re-format inputs (handy right after form submission) | `$(someSelector).autoNumeric('reSet');` |
| `get` | Return the unformatted value as a string | `$(someSelector).autoNumeric('get');` |
| `getLocalized` | Returns the unformatted value, but following the `outputFormat` setting | `$(someSelector).autoNumeric('getLocalized');`  |
| `getNumber` | Return the input unformatted value as a real Javascript number | `$(someSelector).autoNumeric('getNumber');` |
| `getFormatted` | Return the current formatted value | `$(someSelector).autoNumeric('getFormatted');` |
| `getString` | Serialize the whole form input array into a String | `$(someSelector).autoNumeric('getString');` |
| `getArray` | Serialize the whole form input array into an Array | `$(someSelector).autoNumeric('getArray');` |
| `defaults` | Return the default autoNumeric settings | `$.fn.autoNumeric.defaults` |
| `autoFormat` | cf. ES6 Module calls | `$(someSelector).autoFormat('1234.56', {options});` |
| `autoUnFormat` | cf. ES6 Module calls | `$(someSelector).autoUnFormat('1.234,56 €', {options});` |
| `autoValidate` | cf. ES6 Module calls | `$(someSelector).autoValidate({options});` |

#### ES6 Module calls
| Method           | Description | Call example |
| :---------------- | :-----------:  | :-----------:  |
| `getDefaultConfig` | Return the default autoNumeric settings | `an.getDefaultConfig` |
| `format` | Format the given value without needing to initialize an autoNumeric input first | `an.format('1234.56', {options})` |
| `unFormat` | Unformat the given value without needing to initialize an autoNumeric input first | `an.unFormat('1.234,56 €', {options})` |
| `validate` | Check if the given option object is valid, and that each option is valid as well. This throws an error if it's not. | `an.validate({options})` |
| `areSettingsValid` | Return true in the settings are valid | `an.areSettingsValid({options})` |

*Work is ongoing to export all the current jQuery-only methods into the ES6 module.*

## Questions
For questions and support please use the [Gitter chat room](https://gitter.im/autoNumeric/Lobby) or IRC on Freenode #autoNumeric.<br>The issue list of this repo is **exclusively** for bug reports and feature requests.

****

## How to contribute?
Contributors and pull requests are welcome.<br>Feel free to contact us for any questions.

### Get the source
```sh
# git clone -b next https://github.com/BobKnothe/autoNumeric.git
// or the following if you are authentified on github :
// `git clone -b next git@github.com:BobKnothe/autoNumeric.git`
```

### Make your changes
```sh
# cd autoNumeric
```
First things first, in order to be able to compile the ES6 source to something that can be interpreted by the browsers, and get the tools (linter, test runners, etc.) used by the developers, you need to install them by doing :
```sh
# npm install
```

Once you made your changes, you can build the library with :
```sh
# npm run build
```
This will generate the `autoNumeric.js` and `autoNumeric.min.js` in the `dist` folder, that you'll then be able to use in the browsers.

### Run the mandatory tools for linting and testing
We strive to keep the tests green at all times. Hence whenever you change the source, be sure to :
1. Write at least 2 tests :
  - One that validate your change
  - One that invalidate your change
2. Make sure all tests passes on all the supported browsers (PhantomJS, Firefox, and Chrome)
3. Make sure `eslint` does not return any errors regarding the coding style.

##### How to test?
Tests **must always be green** before pushing. Any commit that make the tests fails will be ignored.
To run the tests, you have multiple options :
```sh
// Run unit testing as well as end-to-end testing
# npm run test

// Run unit testing only
# npm run test:unit

// Run end-to-end testing only
# npm run test:e2e

// Run unit testing only...
# npm run test:unitp //...with PhantomJS only
# npm run test:unitf //...with Firefox only
# npm run test:unitc //...with Chrome only
```

##### How to lint?
Linting allow us to keep a coherent code style in all the source files. In order to check that everything is ok, run :
```sh
# npm run lint
```
If any errors are shown, you can try to automatically correct them by running :
```sh
// Use the path of the faulty file there :
# ./node_modules/eslint/bin/eslint.js --fix src/autoNumeric.js
```

#### How to push?
Every changes that you pushed in its own branch in your personal autoNumeric copy should be based on the latest version of `next` branch.

When you create a pull request, make sure to push against the `next` branch.

Your commit must not contain any generated files (ie. files in the `/dist/` directory).<br>
*Note: Generated `dist` files (ie. `autoNumeric.js` and `autoNumeric.min.js`) are built (and force-added to the git repository) only once for each official release on `master`.*

### Dependencies
Currently, autoNumeric depends on jQuery (which is pretty logical since it's a jQuery plugin ;P).<br>
Some work is [in progress](https://github.com/BobKnothe/autoNumeric/issues/244) to provide a jQuery-free version of autoNumeric.

## Older versions
The previous stable autoNumeric version v1.9.46 can be found [here](https://github.com/BobKnothe/autoNumeric/releases/tag/1.9.46).

## Related projects
For integration into [Rails](http://rubyonrails.org/) projects, you can use the [autonumeric-rails](https://github.com/randoum/autonumeric-rails) project.

## Documentation
A more detailed documentation can be found in the [Documentation](Documentation.md) file.<br>
For more examples and an option code generator (that may be outdated), take a look at [here](http://www.decorplanit.com/plugin/).

## Licence
autoNumeric is an [MIT](http://opensource.org/licenses/MIT)-licensed open source project, and its authors are credited in [AUTHORS.md](https://github.com/BobKnothe/autoNumeric/blob/master/AUTHORS.md).

****

Feel free to donate via Paypal [![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=NCW5699RY8NN2) or [Patreon](https://www.patreon.com/user?u=4810062) to support autoNumeric development.
