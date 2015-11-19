# oauth-identity

One of the weaknesses of OpenID Connect is that it conflates the Authorization Server and the Resource Server. 
This leads to challenges when a client needs to call other services which have not been authorized 
by the person to access any identity information. 

OpenID Connect doesn't enable us to map policies to different scopes, as it uses scopes to group user claims. 
The policy is generally limited to "the user (or the organization) approved the release of information."
It doesn't leave a lot of room for the person to set more granular polcies--for example, maybe I only want 
to release information for 12 hours? 

What if instead of the OpenID Connect access token, we were to  use an UMA RPT token? 

Using the UMA RPT would be more conducive for situations where a person needs to share identity information 
within a network of  related clients. 

Also stepped-up authentication is better handled by  UMA, which I think is one of the critical requirements 
for security.  

One other optimization that UMA offers is that the client developer doesn't need to know about scopes. 
Google is publishing a [lot of scopes](http://gluu.co/google-scopes). This reminds me of developers hard 
coding LDAP schema in their code. This leads to a tight bundling of the application with the security 
infrastructure.

A simpler solution would be nice too. How many developers know understand when to use the Hybrid Flow? 
We're torchuring developers with a lot of mumbo-jumbo.

Ever the optimist, I think we can do it faster as we are working with some functional pieces, and we just 
need to fill in some gaps. With UMA Core, OAuth2 Resource Registration, JWT and JOSE, we have many 
of the pieces we need to make a better identity federation stack.

## Requirements

 - Use UMA RPT token instead of OpenID Connect access token
 - No HTTP redirects -- this is one of the weakest points of security
 - Client crypto signing -- its gotten easier, and relying on TLS is not enough.
 
