---
title: Overview
page_title: Overview
description: "Learn the basics when working with the Telerik UI DateInput component for {{ site.framework }}."
previous_url: /helpers/html-helpers/dateinput, /helpers/editors/dateinput/overview
slug: htmlhelpers_dateinput_aspnetcore
position: 1
---

# DateInput Overview

{% if site.core %}
The Telerik UI DateInput TagHelper and HtmlHelper for {{ site.framework }} are server-side wrappers for the Kendo UI DateInput widget.
{% else %}
The Telerik UI DateInput HtmlHelper for {{ site.framework }} is a server-side wrapper for the Kendo UI DateInput widget.
{% endif %}

The DateInput represents an input field that recognizes and formats scheduling values such as dates. It provides separate sections for days, months, years, hours, and minutes, and also supports the customization of date and time formats.

* [Demo page for the DateInput HtmlHelper](https://demos.telerik.com/{{ site.platform }}/dateinput/index)
{% if site.core %}
* [Demo page for the DateInput TagHelper](https://demos.telerik.com/aspnet-core/dateinput/tag-helper)
{% endif %}

## Basic Configuration

The following example demonstrates the basic configuration for the DateInput.

```HtmlHelper
    @(Html.Kendo().DateInput()
        .Name("dateinput") // The name of the DateInput is mandatory. It specifies the "id" attribute of the widget.
        .Value(DateTime.Today) // Set the value of the DateInput.
    )
```
{% if site.core %}
```TagHelper
<kendo-dateinput name="dateinput1" format="MMMM yyyy" value="DateTime.Now">
</kendo-dateinput>
```
{% endif %}

## Events

You can subscribe to all DateInput [events](https://docs.telerik.com/kendo-ui/api/javascript/ui/dateinput#events). For a complete example on basic DateInput events, refer to the [demo on using the events of the DateInput](https://demos.telerik.com/{{ site.platform }}/dateinput/events).

The following example demonstrates how to subscribe to events by a handler name.

```HtmlHelper
    @(Html.Kendo().DateInput()
        .Name("dateinput")
        .Events(e => e
            .Change("dateInput_change")
        )
    )
    <script>
    function dateInput_change() {
        // Handle the change event.
    }
    </script>
```
{% if site.core %}
```TagHelper
<kendo-dateinput name="dateinput" style='width: 100%;' on-change="onChangeHandler">
</kendo-dateinput>

<script>
    function onChangeHandler(e) {
        // Add your logic here.
    }
</script>
```
{% endif %}

### Handling by Template Delegate

The following example demonstrates how to subscribe to events by a template delegate.

```HtmlHelper
    @(Html.Kendo().DateInput()
      .Name("dateinput")
      .Events(e => e
          .Change(@<text>
            function(e) {
                console.log(this.value());
            }
            </text>)
      )
    )
```

## Referencing Existing Instances

To reference an existing Telerik UI DateInput instance, use the [`jQuery.data()`](http://api.jquery.com/jQuery.data/) configuration option. Once a reference is established, use the [DateInput client-side API](https://docs.telerik.com/kendo-ui/api/javascript/ui/dateinput#methods) to control its behavior.

        // Place the following after your Telerik UI DateInput for {{ site.framework }} declaration.
        <script>
        $(function() {
        // The Name() of the DateInput is used to get its client-side instance.
            var dateInput = $("#dateinput").data("kendoDateInput");
        });
        </script>

## See Also

* [Basic Usage of the DateInput HtmlHelper for {{ site.framework }} (Demo)](https://demos.telerik.com/{{ site.platform }}/dateinput/index)
{% if site.core %}
* [Basic Usage of the DateInput TagHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/dateinput/tag-helper)
{% endif %}
* [Using the API of the DateInput HtmlHelper for {{ site.framework }} (Demo)](https://demos.telerik.com/{{ site.platform }}/dateinput/api)
* [Server-Side API](/api/dateinput)
