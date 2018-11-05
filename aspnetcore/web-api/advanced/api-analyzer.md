---
title: Using web API analyzers
author: pranavkm
description: Learn about analyzers in Microsoft.AspNetCore.Mvc.Api.Analyzers
ms.author: pranavkm
ms.custom: mvc
ms.date: 11/5/2018
uid: web-api/api-analyzer
---
# Learn about analyzers in Microsoft.AspNetCore.Mvc.Api.Analyzers

ASP.NET Core 2.2 introduces a NuGet package containing analyzers for web API applications – `Microsoft.AspNetCore.Mvc.Api.Analyzers`. These analyzers work with controllers annotated with <xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute> introduced in ASP.NET Core 2.1, while building on [API conventions](<xref:web-api/action-return-types>).

## Package installation

`Microsoft.AspNetCore.Mvc.Api.Analyzers` can be added with the following approaches:

### [Visual Studio](#tab/visual-studio)

* From the **Package Manager Console** window:
  * Go to **View** > **Other Windows** > **Package Manager Console**
  * Navigate to the directory in which the *ApiConventions.csproj* file exists
  * Execute the following command:

    ```powershell
    Install-Package Microsoft.AspNetCore.Mvc.Api.Analyzers
    ```

* From the **Manage NuGet Packages** dialog:
  * Right-click the project in **Solution Explorer** > **Manage NuGet Packages**
  * Set the **Package source** to "nuget.org"
  * Enter "Microsoft.AspNetCore.Mvc.Api.Analyzers" in the search box
  * Select the "Microsoft.AspNetCore.Mvc.Api.Analyzers" package from the **Browse** tab and click **Install**

### [Visual Studio for Mac](#tab/visual-studio-mac)

* Right-click the *Packages* folder in **Solution Pad** > **Add Packages...**
* Set the **Add Packages** window's **Source** drop-down to "nuget.org"
* Enter "Microsoft.AspNetCore.Mvc.Api.Analyzers" in the search box
* Select the "Microsoft.AspNetCore.Mvc.Api.Analyzers" package from the results pane and click **Add Package**

### [Visual Studio Code](#tab/visual-studio-code)

Run the following command from the **Integrated Terminal**:

```console
dotnet add ApiConventions.csproj package Microsoft.AspNetCore.Mvc.Api.Analyzers
```

### [.NET Core CLI](#tab/netcore-cli)

Run the following command:

```console
dotnet add ApiConventions.csproj package Microsoft.AspNetCore.Mvc.Api.Analyzers
```

---

## Analyzers for API conventions

Open API documents contain each status code and response type an operation may return. In ASP.NET Core MVC, you use attributes such as <xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute> and <xref:Microsoft.AspNetCore.Mvc.ProducesAttribute> to document your operation. <xref:tutorials/web-api-help-pages-using-swagger> goes in to further details on documenting your API.

One of the analyzers in the package, inspects controllers annotated with <xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute> and identifies actions that do not entirely document their responses. Consider the following sample,

[!code-csharp[](api-conventions/sample/Controllers/ContactsController.cs?name=missing404docs&highlight=8-9)]

The action documents the success return type (`200`) but does not document the 404 failure status code. The analyzer reports this as a warning with an option to fix it:

[api-conventions/_static/Analyzer.gif]
