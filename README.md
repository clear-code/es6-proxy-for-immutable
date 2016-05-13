# extended-immutable

Helper library to create extended version of an immutable object, with ES6 Proxy.
See also: http://www.clear-code.com/blog/2016/3/4.html

## Usage

~~~javascript
var immutableObject = {
  originalProperty: true,
  originalMethod: function() {
    return this.originalProperty;
  },
  overriddenMethod: function() {
    return this.originalProperty;
  }
};
immutableObject = Object.freeze(immutableObject);

var proxied = new ExtendedImmutable(immutableObject, {
   addedProperty: true,
   get dynamicProperty() { return this._value; },
   set dynamicProperty(aValue) { return this._value = aValue; },
   overriddenMethod: function() {
     return this.dynamicProperty;
   }
});

proxied.originalProperty; // => true
proxied.addedProperty; // => true
proxied.dynamicProperty; // => undefined
proxied.dynamicProperty = false; // => false
proxied.dynamicProperty; // => false
proxied.originalMethod(); // => true
proxied.overriddenMethod(); // => false
~~~


