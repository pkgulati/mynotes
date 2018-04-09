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


## preserve-content
In _parseChildNodesAnnotations, _parseTemplate is not invoked for a node if it has attribute preserve-content


      // bootstrap the template if it has not already been
      if (this._template && !this._template.content &&
          window.HTMLTemplateElement && HTMLTemplateElement.decorate) {
        HTMLTemplateElement.decorate(this._template);
      }
    },
    
 # Polymer parses template at once...
      _parseTemplate: function(node, index, list, parent) {
      var content = document.createDocumentFragment();
      content._notes = this.parseAnnotations(node);
      content.appendChild(node.content);
      list.push({
        bindings: Polymer.nar,
        events: Polymer.nar,
        templateContent: content,
        parent: parent,
        index: index
      });
      
   ## Loopback relation
   
   ### hasOne
   Contact hasOne Information
   hasOne will create CRUD operation for /api/Contact/id/Information
   then by default (without foreignKey) Information.contactId = Contact.id
   If foreignKey is contactUserId then
   Information.contactUserId = Contact.id
   
   ### belongsTo
   
   Contact belongsTo Information
   Then Only fetch will be created in Contact
   /api/Contacts/id/Information
   Then it will first find Contact.informationId (by default fk will be informationId)
   Query will be id = Contact.informationId
   (here id is primaryKey)
   
   
   
   
   





