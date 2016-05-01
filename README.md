# My Notes 
## Loopback Boot

server.js will call boot method on loopback-boot module

### compile phase
bootLoopBackApp internally calls compile and then execute
Following methods will be called during boat
ConfigLoader.loadAppConfig
ConfigLoader.loadDataSources
ConfigLoader.loadModels

### Execute Phase

setup datasources
setup models
```
 for each model 
        registry.createModel
```
Then invoke boot scripts
    
## Loading and Invoking modules
module exports method are invoked 
var file = require(file);
file(data, options);







