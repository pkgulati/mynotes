# SAML

For Authorization Request.
If Binding is HTTP-POST, then a self submitting form is used. 
Default is redirect, which actually issues a HTTP GET call. 

## SAML vs OAuth2.0 vs OpenID

SAML is usually used for Enterprise Single Sign On.

SAML has one feature that OAuth2 lacks: the SAML token contains the user identity information (because of signing). With OAuth2, you don’t get that out of the box, and instead, the Resource Server needs to make an additional round trip to validate the token with the Authorization Server.

On the other hand, with OAuth2 you can invalidate an access token on the Authorization Server, and disable it from further access to the Resource Server

## Client(Desktop) - Server(TCP server on Unix) using WebSSO
RelayState, is not much applicable here. As there is no state to be stored.
