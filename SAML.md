# SAML

For Authorization Request.
If Binding is HTTP-POST, then a self submitting form is used. 
Default is redirect, which actually issues a HTTP GET call. 

## SAML vs OAuth2.0 vs OpenID

SAML is usually used for Enterprise Single Sign On.

SAML has one feature that OAuth2 lacks: the SAML token contains the user identity information (because of signing). With OAuth2, you don’t get that out of the box, and instead, the Resource Server needs to make an additional round trip to validate the token with the Authorization Server.

On the other hand, with OAuth2 you can invalidate an access token on the Authorization Server, and disable it from further access to the Resource Server

## Client(Desktop) - Server(TCP server on Unix) using WebSSO

https://stackoverflow.com/questions/27917783/desktop-client-application-for-sso-using-saml

RelayState, is not much applicable here. As there is no state to be stored.

## Alternatives
you need a security token service (STS) that issues a SAML token based on your windows identity  (assuming a domain user).  You will have to choose which standard to use for the token flow.  As you say, .NET's WIF has built-in WS-Federation (for browser based authentication) and WS-Trust (for WCF/SOAP based authentication).  I'm assuming you want to secure a .NET web application.  The easiest way is to use WS-Federation (using NETs  WSFederationAuthenticationModule) and setup ADFS server role on your windows domain. Then configure your relying party (your web application) in ADFS and configure the WSFederationAuthenticationModule on your web app to point to ADFS passive signin endpoint.  There are samples on the internet on how to do this
