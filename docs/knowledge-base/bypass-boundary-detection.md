---
title: Bypass Boundary Detection in the ComboBox
page_title: Bypass Boundary Detection in the ComboBox
description: "Learn how to auto-size the popup height in a Kendo UI ComboBox."
previous_url: /controls/editors/combobox/how-to/bypass-boundary-detection, /controls/editors/combobox/how-to/customize/bypass-boundary-detection
slug: howto_bypass_boudary_detection_combobox
tags: telerik, kendo, jquery, combobox, bypass, boudary, detection
component: combobox
type: how-to
res_type: kb
---

## Environment

<table>
 <tr>
  <td>Product</td>
  <td>Progress Kendo UI ComboBox for jQuery</td>
 </tr>
 <tr>
  <td>Operating System</td>
  <td>Windows 10 64bit</td>
 </tr>
 <tr>
  <td>Visual Studio version</td>
  <td>Visual Studio 2017</td>
 </tr>
 <tr>
  <td>Preferred Language</td>
  <td>JavaScript</td>
 </tr>
</table>

## Description

How can I auto-size the popup height in a Kendo UI ComboBox?

## Solution

The following example demonstrates how to achieve the desired scenario.


```dojo
<div id="example" role="application">
<div id="tshirt-view" class="demo-section k-header">
  <h2>Customize your Kendo T-shirt</h2>
  <img id="tshirt" alt="T-shirt image" src="https://demos.telerik.com/kendo-ui/content/web/combobox/tShirt.png" />
  <div id="options">
    <h4>T-shirt Fabric</h4>
    <input id="fabric" placeholder="Select fabric..." />

    <h4>T-shirt Size</h4>
    <select id="size" placeholder="Select size...">
      <option>X-Small</option>
      <option>Small</option>
      <option>Medium</option>
      <option>Large</option>
      <option>X-Large</option>
      <option>2X-Large</option>
      <option>X-Small</option>
      <option>Small</option>
      <option>Medium</option>
      <option>Large</option>
      <option>X-Large</option>
      <option>2X-Large</option>
      <option>X-Small</option>
      <option>Small</option>
      <option>Medium</option>
      <option>Large</option>
      <option>X-Large</option>
      <option>2X-Large</option>
      <option>X-Small</option>
      <option>Small</option>
      <option>Medium</option>
      <option>Large</option>
      <option>X-Large</option>
      <option>2X-Large</option>
    </select>

    <button class="k-button" id="get">Customize</button>
  </div>
</div>
<style scoped>
  .demo-section {
    width: 500px;
    height: 340px;
  }
  .demo-section h2 {
    text-transform: uppercase;
    font-size: 1.2em;
    margin-bottom: 30px;
  }
  .demo-section h4 {
    margin-top: 1.5em;
  }
  #tshirt {
    float: left;
    margin: 0 40px 30px 0;
  }
  #options {
    padding: 20px 0 30px 30px;
  }
  #get {
    margin-top: 25px;
  }
  .k-readonly
  {
    color: gray;
  }
</style>

<script>
  $(document).ready(function() {
    // create ComboBox from input HTML element
    $("#fabric").kendoComboBox({
      dataTextField: "text",
      dataValueField: "value",
      dataSource: [
        { text: "Cotton", value: "1" },
        { text: "Polyester", value: "2" },
        { text: "Cotton/Polyester", value: "3" },
        { text: "Rib Knit", value: "4" }
      ],
      filter: "contains",
      suggest: true,
      index: 3
    });

    // create ComboBox from select HTML element
    $("#size").kendoComboBox({
      open: function() {
        this.options.height = getHeight(this);

        this.refresh();
      }
    });

    function getHeight(widget) {
      var offsetTop = widget.wrapper.offset().top;
      var wndHeight = window.innerHeight;

      var height = parseInt(wndHeight - offsetTop - 30);

      if (isNaN(height)) {
        height = 200;  
      }

      return height;
    }

    var fabric = $("#fabric").data("kendoComboBox");
    var select = $("#size").data("kendoComboBox");


    $("#get").click(function() {
      alert('Thank you! Your Choice is:\n\nFabric ID: ' + fabric.value() + ' and Size: ' + select.value());
    });
  });
</script>
</div>
```

## See Also

* [ComboBox JavaScript API Reference](/api/javascript/ui/combobox)
* [How to Bypass Boundary Detection]({% slug howto_bypass_boudary_detection_combobox %})
* [How to Configure Deferred Value Binding]({% slug howto_configure_deffered_value_binding_combobox %})
* [How to Implement Cascading with Local Data]({% slug howto_implement_cascading_local_data_combobox %})
* [How to Make Visible Input Readonly]({% slug howto_make_visible_inputs_readonly_combobox %})
* [How to Open ComboBox When onFocus is Triggered]({% slug howto_open_onfocus_combobox %})
* [How to Prevent Adding Custom Values]({% slug howto_prevent_adding_custom_values_combobox %})
* [How to Underline Matched Search]({% slug howto_underline_matched_search_combobox %})
