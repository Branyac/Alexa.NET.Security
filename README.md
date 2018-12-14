# Alexa.NET.Security
This is a middleware library to authenticate requests sent to an Alexa ASP.NET backend. 
It wraps the verification logic of the [Alexa Skills SDK for .NET](https://github.com/timheuer/alexa-skills-dotnet) in an easy to use middleware.

It will take care of almost all additional [security requirements](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-web-service#verifying-that-the-request-was-sent-by-alexa) for self-hosted skills:
- [x] Check the request signature to verify the authenticity of the request.
- [x] Check the request timestamp to ensure that the request is not an old request being sent as part of a “replay” attack.
- [x] Validate the signature in the HTTP headers
- [x] Verify the URL specified by the `SignatureCertChainUrl`
- [x] The signing certificate has not expired (examine both the Not Before and Not After dates)
- [x] The domain echo-api.amazon.com is present in the Subject Alternative Names (SANs) section of the signing certificate
- [x] All certificates in the chain combine to create a chain of trust to a trusted root CA certificate
- [x] Verify request body hash value


# Getting Started

## Add ASP.NET Core 2.0 Middleware
Install from [NuGet](https://www.nuget.org/packages/Alexa.NET.Security.Middleware/)

`Install-Package Alexa.NET.Security.Middleware`

```csharp
// Startup.cs
using Alexa.NET.Security.Middleware;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //...
    app.UseAlexaRequestValidation();
    app.UseMvc();
}
```
