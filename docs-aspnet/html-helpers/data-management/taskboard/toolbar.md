---
title: Toolbar
page_title: Toolbar
description: "Get started with the Telerik UI for {{ site.framework }} TaskBoard and learn how to configure its toolbar."
slug: htmlhelpers_taskboard_aspnetcore_toolbar
position: 9
---

# Toolbar

By default, the toolbar of the TaskBoard displays the `addColumn` and the `search` tools. Default tools can be excluded, or custom tools can be added through the `Toolbar` configuration. 

## Custom Tools

The `Toolbar Items` configuration allows you to set the desired tools that will be rendered in the toolbar of the TaskBoard.

The following example demonstrates how to add a custom tool to the toolbar.

```HtmlHelper
    <script>
        kendo.ui.taskboard.commands["CustomAddCardCommand"] = kendo.ui.taskboard.Command.extend({
            exec: function () {
                var taskboard = this.taskboard;
                var options = this.options;
                taskboard.addCard({ Status: "todo", Title: "Add Title", Description: "Add Description", Color: "green" });
                taskboard.dataSource.sync();
            }
        });
    </script>

    @(Html.Kendo().TaskBoard()
        .Name("taskBoard")
        .Toolbar(t => t.Items(items =>
        {
            items.Add().Type("button").Command("CustomAddCardCommand").Name("addCard").Text("Add New Card").Icon("plus");
            items.Add().Type("spacer");
            items.Add().Type("TaskBoardSearch").Command("SearchCommand").Name("search").Text("Search").Icon("search");
        }))
        .Columns(c =>
        {
            c.Add().Text("To-do").Status("todo");
            c.Add().Text("In Progress").Status("inProgress");
            c.Add().Text("Done").Status("done");
        })
        .DataDescriptionField("Description")
        .DataStatusField("Status")
        .DataTitleField("Title")
        .DataOrderField("Order")
        .BindTo((IEnumerable<Kendo.Mvc.Examples.Models.TaskBoard.CardViewModel>)ViewBag.Cards)
    )
```

## See Also

* [Overview of the TaskBoard (Demo)](https://demos.telerik.com/kendo-ui/taskboard/index)
* [JavaScript API Reference of the TaskBoard](https://docs.telerik.com/kendo-ui/api/javascript/ui/taskboard)
