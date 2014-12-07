jQuery SimplePassMeter
----

SimplePassMeter is a
<a href='http://plugins.jquery.com/project/simplePassMeter' title='Go to the jQuery plug-in page'>jQuery plug-in</a>
that makes checking the requirements for - and the strength of -
passwords much easier. Everything is ready to go out of the box, or
you can configure many of the pieces to make this plug-in exactly
what you need.
  
**Requires jQuery 1.2+**
  
**Features**
* Simple to implement
* Displays password requirement violations as well as strength
* Completely customizable
* Supports custom password requirements
* 7.9 Kb minified


### Options and Features

**_All options_**

```text
'showOnFocus': BOOLEAN      If true, only shows the password strength meter UI when the field
                            is focused
'showOnValue': BOOLEAN      If true, only shows the password strength meter UI when the field
                            has some value (in other words, once the user has typed something),
                            this is regardless of any focus
'location': STRING          Location of the meter UI, one of 't'op, 'b'ottom, 'l'eft, or
                            'r'ight. NOTE that 't'op is not very reliably placed, and could
                            overflow into your field.
'offset': NUMBER            Pixels that the meter UI is offset from the password field.
'container': STRING         jQuery selector for the containing element you want the UI to be in.
                            NOTE: this disables absolute positioning and thus makes the
                            'location' and 'offset' fields obsolete.

'requirements': OBJECT      All requirements that the password must fulfill, an object with
                            sub-objects. Each requirement should have a unique key, and be
                            itself an object with various members (see below). You can specify
                            only some of the members in order to use the other default members;
                            for example, specify the "minLength" requirement, but only the
                            "value" member thus using the default "callback" function.
                            
  'requirementName': OBJECT A requirment specification, the name of the requirement is the key
                            for the "requirements" option object.
                            
    'value': VARIOUS,       The "value" for any requirement must evaluate to true (no zero, no
                            false, no null), but can be requirement-specific as in the
                            "minLength" case where the number of characters is used. In others
                            where the value is not specific use a simple boolean true.
                            
    'regex': STRING,        If the user's input matches the regex, the requirement is
                            considered passed.
                            
                            *** NOTE: Use "regex" OR "callback", not both.
                            
    'callback': FUNCTION,   If a requirement specifies a "callback" then this function will be
                            called with two arguments - the input from the user and value for
                            this requirement - to test whether the current input fulfills the
                            requirement. The function should return the boolean true if it does,
                            false otherwise.
                            
    'message': STRING       The message to display to the user if they do not meet the
                            requirement. It can contain the special sequence "%V" (without
                            quotes) which will be replaced by the value parameter for this
                            requirement.

'ratings': ARRAY            The categories for the ratings, an array of objects. When an input
                            hits the "minScore" for a given rating, its values will be used.
                            NOTE THAT THESE MUST BE IN ORDER BY THE "minScore" ATTRIBUTE.
  OBJECT:
    'minScore': NUMBER,     The minimum score to hit to trigger this rating.
    
    'className': STRING,    The CSS class to place on the "simplePassMeter" div when this rating
                            is used.
                            
    'text': STRING          The text to place in the meter UI when this rating is triggered.
```

**_Built-in Requirements_**


These requirements are already built-in, just specify them in the
'requirements' block of your options object to turn them on. 
See the <a href='http://jordankasper.com/jquery/meter/examples'>Examples</a> page for details on common usage.

<table>
  <thead>
    <tr>
        <th style='width: 20%'>Name</th>
        <th style='width: 40%'>Description</th>
        <th>Sample Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>minLength</td>
        <td>Minimum length</td>
        <td>'minLength': { 'value': 6 }</td>
    </tr>
    <tr>
        <td>noMatchField</td>
        <td>The password cannot match the value of the given field</td>
        <td>'noMatchField': { 'value': '#username' }</td>
    </tr>
    <tr>
        <td>matchField</td>
        <td>The password MUST match the value of the given field</td>
        <td>'matchField': { 'value': '#verify' }</td>
    </tr>
    <tr>
        <td>letters</td>
        <td>Password must contain at least one letter</td>
        <td>'letters': { 'value': true }</td>
    </tr>
    <tr>
        <td>numbers</td>
        <td>Password must contain at least one number</td>
        <td>'numbers': { 'value': true }</td>
    </tr>
    <tr>
        <td>lower</td>
        <td>Password must contain at least one lower-case letter</td>
        <td>'lower': { 'value': true }</td>
    </tr>
    <tr>
        <td>upper</td>
        <td>Password must contain at least one upper-case letter</td>
        <td>'upper': { 'value': true }</td>
    </tr>
    <tr>
        <td>special</td>
        <td>Password must contain at least one special character</td>
        <td>'special': { 'value': true }</td>
    </tr>
  </tbody>
</table>

**_Built-in Ratings_**

These ratings are already built-in, they will be used unless you
override them. See the <a href='http://jordankasper.com/jquery/meter/examples'>Examples</a> page for
details on specifying your own ratings.
  
<table>
  <thead>
    <tr>
        <th style='width: 15%'>Score Threshold</th>
        <th style='width: 15%'>Class Name</th>
        <th>Meter Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>0</td>
        <td>meterFail</td>
        <td>You need a stronger password</td>
    </tr>
    <tr>
        <td>25</td>
        <td>meterWarn</td>
        <td>Your password is a bit weak</td>
    </tr>
    <tr>
        <td>50</td>
        <td>meterGood</td>
        <td>Your password is good</td>
    </tr>
    <tr>
        <td>75</td>
        <td>meterExcel</td>
        <td>Great password!</td>
    </tr>
  </tbody>
</table>

**_Style Options_**

The simplePassMeter UI is completely CSS driven using standard
XHTML tags, classes, and IDs. Below is a sample styling, but
this is by far not the most you can do.

```html
<div class="simplePassMeter meterGood" id="ex1_simplePassMeter">
  <p>
    <span class="simplePassMeterIcon" />
    <span class="simplePassMeterText">Your password is good</span>
  </p>
  <div class="simplePassMeterBar">
    <div class="simplePassMeterProgress" />
  </div>
</div>
```

```css
.simplePassMeter {
  border: 1px solid #aaa;
  background-color: #f3f3f3;
  color: #666;
  font-size: 0.8em;
  padding: 1px 5px 0 5px;
  margin: 0;
  width: 19em;
}

.meterFail { border: 1px solid #daa; background-color: #fdd; }
.meterWarn { border: 1px solid #fd6; background-color: #feb; }
.meterGood { border: 1px solid #ada; background-color: #dfd; }
.meterExcel { border: 1px solid #aad; background-color: #ddf; }

.simplePassMeterBar { background-color: #ddd; }
.meterFail .simplePassMeterProgress  { background-color: #f66; }
.meterWarn .simplePassMeterProgress  { background-color: #fd6; }
.meterGood .simplePassMeterProgress  { background-color: #ada; }
.meterExcel .simplePassMeterProgress { background-color: #88f; }
```

### Basic Usage

```html
<input type='password' id='myPassword' name='myPassword' />
```

```js
$('#myPassword').simplePassMeter();
```

#### Adding in a few custom requirements...

```js
$('#myPassword').simplePassMeter({
  'requirements': {
    'minLength': {'value': 10},  // at least 10 characters
    'lower': {'value': true},    // at least 1 lower-case letter
    'upper': {'value': true},    // at least 1 upper-case letter
    'special': {'value': true}   // at least 1 special character
  }
});
```

You can find [more examples](http://jordankasper.com/jquery/meter/examples) on my personal site.
  
### Tested Browsers

* Mozilla Firefox 2/3
* Microsoft Internet Explorer 7/8
* Google Chrome
* Opera
