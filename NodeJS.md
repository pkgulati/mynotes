### lib/internal/modules/cjs/loader.js
This file has methods like Module._compile,

## General
Before node.js file is run, lib/internal/bootstrap/loaders.js gets run first to bootstrap the internal binding and module loaders, including process.binding(), process._linkedBinding(), internalBinding() and NativeModule. 
And then { internalBinding, NativeModule } will be passed into this bootstrapper to bootstrap Node.js core.
