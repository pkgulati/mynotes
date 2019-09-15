# SAML

For Authorization Request.
If Binding is HTTP-POST, then a self submitting form is used. 
Default is redirect, which actually issues a HTTP GET call. 

## SAML vs OAuth2.0 vs OpenID
SAML is better suited for Enterprise Single Sign On.

## Client(Desktop) - Server(TCP server on Unix) using WebSSO
RelayState, is not much applicable here. As there is no state to be stored.
