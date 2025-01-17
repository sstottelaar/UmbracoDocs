---
versionFrom: 9.0.0
---

# Rendering Forms Scripts

Forms output some JavaScript which is by default rendered right below the markup.

In many cases, you might prefer rendering your scripts at the bottom of the page, e.g. before the closing `</body>` tag, as this generally improves site performance.

In order to render your scripts where you want, you need to add the following snippet to your template. Make sure you add it below your scripts, right before the closing `</body>` tag:

```csharp
@using Umbraco.Forms.Web.Extensions;

@if (TempData["UmbracoForms"] != null)
{
    foreach (var form in TempData.Get<List<Guid>>("UmbracoForms"))
    {
        @await Component.InvokeAsync("RenderFormScripts", new {formId = form, theme = "bootstrap3-horizontal"})
    }
}
```

## Enabling `ExcludeScripts`

Whether you are inserting your Form using a macro or adding it directly in your template, you need to make sure `ExcludeScripts` is checked/enabled:

To enable `ExcludeScripts`:

- Using the **Insert Form with Theme** macro:

    ![Exclude scripts](images/exclude-scripts-v9.png)

- While inserting Forms **directly** in your template:

    ```csharp
    @await Umbraco.RenderMacroAsync("renderUmbracoForm", new {FormGuid="6c3f053c-1774-43fa-ad95-710a01d9cd12", FormTheme="bootstrap3-horizontal", ExcludeScripts="1"})
    ```

---

Prev: [Preparing your Frontend](../Prepping-Frontend/index.md) &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; Next: [Themes](../Themes/index.md)
