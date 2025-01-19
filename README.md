﻿Resend .NET SDK
==========================================================================

[![CI](https://github.com/resend/resend-dotnet/workflows/CI/badge.svg)](https://github.com/resend/resend-dotnet/actions)
[![NuGet](https://img.shields.io/nuget/vpre/resend.svg?label=NuGet)](https://www.nuget.org/packages/Resend/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

.NET library for the Resend API.


Install
--------------------------------------------------------------------------

```
> dotnet add package Resend
```


Examples
--------------------------------------------------------------------------

Send email with:

* [ASP.NET - Minimal API](https://github.com/resend/resend-dotnet/tree/master/examples/WebMinimalApi)
* [ASP.NET - Razor](https://github.com/resend/resend-dotnet/tree/master/examples/WebRazor)
* [Console app](https://github.com/resend/resend-dotnet/tree/master/examples/ConsoleNoDi)


Setup
--------------------------------------------------------------------------

First, you need to get an API key, which is available in the
[Resend Dashboard](https://resend.com/).

In the startup of your application, configure the DI container as follows:

```csharp
using Resend;

builder.Services.AddOptions();
builder.Services.AddHttpClient<ResendClient>();
builder.Services.Configure<ResendClientOptions>( o =>
{
    o.ApiToken = Environment.GetEnvironmentVariable( "RESEND_APITOKEN" )!;
} );
builder.Services.AddTransient<IResend, ResendClient>()
```

You can then use the injected `IResend` instance to send emails.


Usage
--------------------------------------------------------------------------

Send your first email:

```csharp
using Resend;

public class FeatureImplementation
{
    private readonly IResend _resend;


    public FeatureImplementation( IResend resend )
    {
        _resend = resend;
    }


    public Task Execute()
    {
        var message = new EmailMessage();
        message.From = "you@example.com";
        message.To.Add( "user@gmail.com" );
        message.Subject = "hello world";
        message.TextBody = "it works!";

        await _resend.EmailSendAsync( message );
    }
}
```


Send email using HTML
--------------------------------------------------------------------------

Send an email custom HTML content:

```csharp
using Resend;

public class FeatureImplementation
{
    private readonly IResend _resend;


    public FeatureImplementation( IResend resend )
    {
        _resend = resend;
    }


    public Task Execute()
    {
        var message = new EmailMessage();
        message.From = "you@example.com";
        message.To.Add( "user@gmail.com" );
        message.Subject = "hello world";
        message.HtmlBody = "<strong>it works!</strong>";

        await _resend.EmailSendAsync( message );
    }
}
```


License
--------------------------------------------------------------------------

MIT License