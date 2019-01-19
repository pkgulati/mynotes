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
       If we define  "primaryKey" : "xyz", "foreignKey" : "contactUserId"
       Then it will be where Information.xyz = Contact.contactUserId
       
   
### OAuth or SSL

https://stackoverflow.com/questions/29636715/oauth-2-0-two-legged-authentication-vs-ssl-tls

OAuth and SSL\TLS are two separate layers of the OSI model. OAuth is for authentication and is at the top in Layer 7 while SSL\TLS is for transport security in layer 4. It's easy to confuse SSL with client certificates because they both use PKI.

You are correct in your understanding of OAuth...it is used for authorizing individuals not organizations\servers. 2-legged OAuth is a term that is thrown around which encompass various alternate OAuth flows, all of which do not follow a standard.

In my opinion, you want to use client certificates to secure your server-server communication...all that is really required is a single x509 certificate that can be used as both SSL (transport security) and client certificate (authorization); although using 2 certificates is the norm.
   
   





