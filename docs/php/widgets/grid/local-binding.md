---
title: Local Binding
page_title: Local Binding | Grid PHP Class
description: "Bind Kendo UI Grid PHP class to an array of data."
slug: localbinding_grid_uiforphp
position: 2
---

# Local Binding

This article shows how to bind a Kendo UI Grid for PHP to a PHP [array](http://php.net/manual/en/language.types.array.php). This array can be populated from a database or declared inline (in the page). Local binding means that all data operations&mdash;paging, sorting, filtering, etc.&mdash;happens on the client-side.

## Approaches

This PHP array can be populated from a database, or declared inline (in the page). Local binding means that all data operations&mdash;paging, sorting, filtering, etc.&mdash;happen on the client side.

### Bind to PDO-Returned Arrays

[PHP Data Objects (PDO)](http://www.php.net/manual/en/intro.pdo.php) is an interface for accessing various databases in PHP.

Below are listed the steps for you to follow when binding the Kendo UI Grid for PHP to an array returned by PDO.

> **Important**
>
> The following demo is using the sample SQLite database shipped with the Telerik UI for PHP demos (`/wrappers/php/sample.db`).

**Step 1** Make sure you followed all the steps from the [introductory article on Telerik UI for PHP]({% slug overview_uiforphp %})&mdash;include the autoloader, JavaScript, and CSS files.

**Step 2** Create a PDO connection.



        <?php
        $db = new PDO('sqlite:../sample.db');
        ?>

**Step 3** Retrieve all records from the **Products** table.



        <?php
        $statement = $db->prepare('SELECT * FROM Products');
        $statement->execute();
        $products = $statement->fetchAll(PDO::FETCH_ASSOC);
        ?>

**Step 4** Create a [data source](/api/php/Kendo/Data/DataSource) and set its [`data`](/api/php/Kendo/Data/DataSource#data) and [`schema`](/api/php/Kendo/Data/DataSource#schema). Setting the `schema` is required to specify the model fields. These fields are required for filtering and editing.



        <?php
        // Create the schema model
        $model = new \Kendo\Data\DataSourceSchemaModel();

        // Create a field for the 'ProductName' column of the 'Products' table
        $productNameField = new \Kendo\Data\DataSourceSchemaModelField('ProductName');
        $productNameField->type('string');

        // Create a field for the 'UnitPrice' column of the 'Products' table
        $unitPriceField = new \Kendo\Data\DataSourceSchemaModelField('UnitPrice');
        $unitPriceField->type('number');

        // Create a field for the 'Discontinued' column of the 'Products' table
        $discontinuedField = new \Kendo\Data\DataSourceSchemaModelField('Discontinued');
        $discontinuedField->type('boolean');

        $model->addField($productNameField, $unitPriceField, $discontinuedField);

        // Create the schema
        $schema = new \Kendo\Data\DataSourceSchema();

        // Set its model
        $schema->model($model);

        // Create the data source
        $dataSource = new \Kendo\Data\DataSource();

        // Specify the schema and data
        $dataSource->data($products)
                   ->schema($schema);
        ?>

**Step 5** Create a [Grid](/api/php/Kendo/UI/Grid), configure its [columns](/api/php/Kendo/UI/Grid#addcolumn) and set its [data source](/api/php/Kendo/UI/Grid#datasource).



        <?php
        $grid = new \Kendo\UI\Grid('grid');

        $productNameColumn = new \Kendo\UI\GridColumn();
        $productNameColumn->field('ProductName')
                          ->title('Product Name');

        $unitPriceColumn = new \Kendo\UI\GridColumn();
        $unitPriceColumn->field('UnitPrice')
                        ->width('130px')
                        ->format('{0:c}')
                        ->title('Unit Price');

        $discontinuedColumn = new \Kendo\UI\GridColumn();
        $discontinuedColumn->field('Discontinued')
                           ->width('130px');

        $grid->addColumn($productNameColumn, $unitPriceColumn, $discontinuedColumn)
             ->dataSource($dataSource);
        ?>

**Step 6** Output the Grid by echoing the result of the `render` method.



        <?php
        echo $grid->render();
        ?>

### Use DataSourceResult Helpers

The `DataSourceResult` class is a helper utility on top of PDO which simplifies common CRUD operations. It is distributed with the Telerik UI for PHP demos and can be found in the `/wrappers/php/lib/` directory of the Telerik UI for PHP distribution.

**Step 1** Make sure you followed all the steps from the [introductory article on Telerik UI for PHP]({% slug overview_uiforphp %})&mdash;include the autoloader, JavaScript, and CSS files.

**Step 2** Copy `/wrappers/php/lib/DataSourceResult.php` to your website root and include it.



        <?php require_once 'lib/DataSourceResult.php'; ?>

**Step 3** Create a new instance of the `DataSourceResult` and use its `read` method to retrieve data from the database.



        <?php
        // The constructor accepts the PDO DSN for the target database
        $result = new DataSourceResult('sqlite:../sample.db');

        // The 'read' method accepts table name and array of columns to select.
        $data = $result->read('Products', array('ProductName', 'UnitPrice', 'Discontinued'));
        // The result of the 'read' method is an array with two elements 'data' and 'total'.
        ?>

**Step 4** Configure a `DataSource` and `schema`.



        <?php
        // Create the schema model
        $model = new \Kendo\Data\DataSourceSchemaModel();

        // Create a field for the 'ProductName' column of the 'Products' table
        $productNameField = new \Kendo\Data\DataSourceSchemaModelField('ProductName');
        $productNameField->type('string');

        // Create a field for the 'UnitPrice' column of the 'Products' table
        $unitPriceField = new \Kendo\Data\DataSourceSchemaModelField('UnitPrice');
        $unitPriceField->type('number');

        // Create a field for the 'Discontinued' column of the 'Products' table
        $discontinuedField = new \Kendo\Data\DataSourceSchemaModelField('Discontinued');
        $discontinuedField->type('boolean');

        $model->addField($productNameField, $unitPriceField, $discontinuedField);

        // Create the schema
        $schema = new \Kendo\Data\DataSourceSchema();

        // Set its model and describe the data format.
        $schema->model($model)
               ->data('data')
               ->total('total');

        // Create the data source
        $dataSource = new \Kendo\Data\DataSource();

        // Specify the schema and data
        $dataSource->data($data)
                   ->schema($schema);
        ?>

**Step 5** Create a Grid, configure its columns and set its `DataSource`.



        <?php
        $grid = new \Kendo\UI\Grid('grid');

        $productNameColumn = new \Kendo\UI\GridColumn();
        $productNameColumn->field('ProductName');

        $unitPriceColumn = new \Kendo\UI\GridColumn();
        $unitPriceColumn->field('UnitPrice');

        $discontinuedColumn = new \Kendo\UI\GridColumn();
        $discontinuedColumn->field('Discontinued');

        $grid->addColumn($productNameColumn, $unitPriceColumn, $discontinuedColumn);
        ?>

**Step 6** Output the Grid by echoing the result of the `render` method.



        <?php
        echo $grid->render();
        ?>

## See Also

* [Overview of the Grid PHP Class]({% slug overview_grid_uiforphp %})
* [Remote Binding of the Grid PHP Class]({% slug remotebinding_grid_uiforphp %})
* [Editing of the Grid PHP Class]({% slug editing_grid_uiforphp %})
* [Overview of the Kendo UI Grid Widget]({% slug overview_kendoui_gantt_widget %})
* [Telerik UI for PHP API Reference Folder](/api/php/Kendo/UI/AutoComplete)
* [Telerik UI for PHP Classes Folder]({% slug overview_autocomplete_uiforphp %})
