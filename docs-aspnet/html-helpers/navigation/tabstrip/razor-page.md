---
title: Razor Page
page_title: Razor Page
description: "An example on how to configure the Telerik UI TabStrip component for {{ site.framework }} in a Razor Page."
slug: htmlhelpers_tabstrip_aspnetcore_razor_page
---

# Razor Page

This article demonstrates how to add the Telerik UI TabStrip for {{ site.framework }} to a RazorPage and load content via AJAX.

For the full project with RazorPages examples, visit our [GitHub repository](https://github.com/telerik/ui-for-aspnet-core-examples/tree/master/Telerik.Examples.RazorPages).

```tab-HtmlHelper(csthml)        
    @inject Microsoft.AspNetCore.Antiforgery.IAntiforgery Xsrf
    @Html.AntiForgeryToken()

    <div class="wrapper">
        @(Html.Kendo().TabStrip()
            .Name("tabstrip")
            .Items(tabstrip =>
            {
                tabstrip.Add().Text("Dimensions & Weights")
                    .Selected(true)
                    .LoadContentFrom(Url.Content("~/Content/TabStrip/ajaxContent1.html"));
                tabstrip.Add().Text("Engine")
                    .LoadContentFrom(Url.Content("~/Content/TabStrip/ajaxContent2.html"));
                tabstrip.Add().Text("Chassis")
                    .LoadContentFrom(Url.Content("~/Content/TabStrip/ajaxContent3.html"));
            })
        )
    </div>
	
```
{% if site.core %}
```TagHelper
<kendo-tabstrip name="tabstrip">
    <items>
        <tabstrip-item text="Dimensions & Weights"
                       selected="true"
                       content-url="@Url.Content("~/Content/TabStrip/ajaxContent1.html")">
        </tabstrip-item>
        <tabstrip-item text="Engine"
                        content-url="@Url.Content("~/Content/TabStrip/ajaxContent2.html")">
        </tabstrip-item>
        <tabstrip-item text="Chassis "
                       content-url="@Url.Content("~/Content/TabStrip/ajaxContent3.html")">
        </tabstrip-item>
    </items>
</kendo-tabstrip>
```
{% endif %}
```tab-PageModel(cshtml.cs)      
	
    public void OnGet()
    {

    }
    
```
