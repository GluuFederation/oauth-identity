# oauth-identity

One of the weaknesses of OpenID Connect is that the OpenID Provider (OP) conflates the Authorization Server and the Resource Server. This leads to challenges when the OpenID Connect Relying Party (RP) needs to call API's which are not themselves clients of the OP. Consider the diagram below:

<img src="https://raw.githubusercontent.com/GluuFederation/oauth-identity/master/img/Multi-API%20Backend.png" width="400">

What if the /doSomething API needs information about the user that is not known by the 
original Relying Party? There is no way to create policy in the OP to allow the /doSomething API to gather the required claims!

OpenID Connect doesn't enable us to map policies to different scopes, as it uses scopes to group user claims. The policy is generally limited to "the user (or the organization) approved the release of information." It doesn't leave a lot of room for the person to set more granular polcies--for example, maybe I only want to release information for 12 hours?

OpenID Connect also has problems when identity information resides on more than one OpenID Provider. While OpenID Connect has some mention of [Aggregated and Distributed Claims] (http://openid.net/specs/openid-connect-core-1_0.html#AggregatedDistributedClaims), it is not well flushed out.

What if instead of the OpenID Connect access token, we were to  use an UMA RPT token to protect a user_info-like endpoint?

Using the UMA RPT would be more conducive for situations where a person needs to share identity information within a network of  related clients. 

Also stepped-up authentication is better handled by  UMA, which I think is one of the critical requirements for security.  

One other optimization that UMA offers is that the client developer doesn't need to know about scopes. Google is publishing a [lot of scopes](http://gluu.co/google-scopes). This reminds me of developers hard coding LDAP schema in their code. This leads to a tight bundling of the application with the security infrastructure.

A simpler identity federation solution would be nice too. How many developers  understand the OpenID Connect Hybrid Flow, and when to use it? We're torchuring developers with a lot of mumbo-jumbo.

While OpenID Connect took five years to develop, ever the optimist, I think we create a new identity federation standard  faster than that, as we are working with some functional pieces, and we just need to fill in some gaps. With UMA Core, OAuth2 Resource Registration, JWT and JOSE, we have many of the pieces we need to make a more functionaly identity federation stack for today's micorservices / cloud infastructure.

## Requirements

 - Use UMA RPT token instead of OpenID Connect access token to protect user_info endpoint
 - No HTTP redirects -- this is one of the weakest points of security
 - Minimal optionality
 - Client signing as profile


