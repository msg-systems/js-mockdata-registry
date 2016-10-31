# js-mockdata-registry

JavaScript registry or mockdata

<p/>
<img src="https://nodei.co/npm/js-mockdata-registry.png?downloads=true&stars=true" alt=""/>

<p/>
<img src="https://david-dm.org/msg-systems/js-mockdata-registry.png" alt=""/>

## Purpose
The `js-mockdata-registry` is a small registry for mockdata objects that should be references within other mockdata objects.

## Getting started

Simply add the `js-mockdata-registry` to your package.json file and use `npm install` for installation.

```json
		"devDependencies": {
		    "js-mockdata-registry":        "~1.0.0"
		}
```

Once it is installed you can `require` the module.

```js
		let mockdata = require('js-mockdata-registry')
```

## Usage

This chapter explains the basic usage of the registry.

### Mockdata interface

| Method | Description |
| --- | --- | --- |
| addObject (Object obj) | Adds the given object to the registry. The object must have the attribute `mark` with a unique value within the registry. The `mark`is consumed in the registration process. An error is throw if either the attribute `mark` is not exisiting or if its value is not unique |
| hasObject (String mark) : Boolean | Checks the registry if an object with the given `mark` exists|
| getObject (String mark) | Reads the desired registry entry for the given `mark`. Throws an error if the given mark is not existing in the registry. |
| removeObject (String mark) | Removes the desired registry entry for the given `mark`. Throws an error if the given mark is not existing in the registry. |
| log (Number depth) | Outputs the current registry using node's `util.inspect` function. The `depth` is handed over to the inspect function. |
| resolve (Object resultObj, Object obj, String attrib) | This function resolves an object reference to an registry entry. The originial `obj` won't be changed during resolve. Instead the `resultObj` will be altered. For more details see the examples. |
    

### Example usage

```js
/* in order to add objects we have to instanciate the registry */
let mockdata = require('js-mockdata-registry')

/* adding objects                                              */
mockdata.registry.addObject({
    mark: 'User.John',
    firstname: 'John',
    lastname: 'Doe'
})

/* reading objects                                             */
mockdata.registry.getObject('User.John')

/* resolving references                                        */
// define the new object with a objectRef to an existing mark
let project = {
	desc: 'first project',
    supervisor: { objectRef: 'User.John' }
}
// clone the base object
let resolvedProject = Object.assign({}, project)
// let the registry resolve the object reference 
mockdata.registry.resolve(resolvedProject, project, 'supervisor')


```
