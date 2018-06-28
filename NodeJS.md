### require
require will treat internal modules and user modules differently.
For Native module NativeModule.require will get invoked, which internally will call NativeModule.compile
For User Modules and Module.prototype.load will get called (after create of new Module)
Module.load will call extension handlers based on extension, like for .js file 

### .js extension handler
Following method is called to load user module js file
```
Module._extensions['.js'] = function(module, filename) {
  var content = fs.readFileSync(filename, 'utf8');
  module._compile(stripBOM(content), filename);
};
```
### Module._compile
This is called by js extension handler 

### lib/internal/modules/cjs/loader.js
This file has methods like Module._compile,

## General
Before node.js file is run, lib/internal/bootstrap/loaders.js gets run first to bootstrap the internal binding and module loaders, including process.binding(), process._linkedBinding(), internalBinding() and NativeModule. 
And then { internalBinding, NativeModule } will be passed into this bootstrapper to bootstrap Node.js core.
