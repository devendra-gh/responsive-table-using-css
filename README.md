## responsive-table-using-css
###Objective:
It’s not easy adapting tables to a responsive layout. Either some rows or columns will have to be cropped, which disrupts the visitor or the table will have to be shrunk to fit a small screen, making it incomprehensible. Both these options just beat the purpose of a responsive website being user-friendly, especially if the data table is particularly large. Our goal was to meet the following requirements:

1. No javascript. You can find all sorts of plugins to but it’s nice to go with a pure CSS solution if at all possible.
2. No adjusting the font-size and spacing.
3. The text must be localized so no storing plain text in the stylesheets.

####How to achieve responsive table:

#####Step 1: 
Use data-* attribute (data-title) to hold information about the column header(s) associated with the markup. Pseudo elements, specifically :before or :after, match the virtual first and last children of the selected element.

#####eg:
```HTML
<td data-title="User ID">0001</td>
```

#####Step 2:
When the screen is below a certain threshold, set the table elements to display: block, hide the thead where assistive tech won’t see it, and use generated content to expose the data-* attributes. 

#####eg:
```HTML
.table-responsive td:before {
       content: attr(data-title);
   }
```
#####So the following basic Table structure is:

<div class="table-responsive">
   <table>
       <thead>
       <tr>
           <th>User ID</th>
           <th>First Name</th>
           <th>Last Name</th>
           <th>Username</th>
       </tr>
       </thead>
       <tbody>
       <tr>
           <td data-title="User ID">0001</td>
           <td data-title="First Name">Maria</td>
           <td data-title="Last Name">Anders</td>
           <td data-title="Username">@maria</td>
       </tr>
   </tbody>
</table>
</div>


#####And following CSS styles media query is:

table {
   width: 100%;
   text-align: left;
}

@media only screen and (max-width: 768px) {

   .table-responsive table,
   .table-responsive thead,
   .table-responsive tbody,
   .table-responsive tfoot,
   .table-responsive tr,
   .table-responsive th,
   .table-responsive td {
       display: block;
   }

   .table-responsive thead tr {
       position: absolute;
       top: -9999px;
       left: -9999px;
   }

   .table-responsive tfoot tr > th {
       position: absolute;
       top: -9999px;
       left: -9999px;
   }

   .table-responsive tr {
       border: 1px solid #ccc;
   }

   .table-responsive td {
       border: none;
       border-bottom: 1px solid #eee;
       position: relative;
       white-space: normal;
       text-align: left;
       padding: 5px 10px 5px calc(50% + 10px);
   }

   .table-responsive td:before {
       content: attr(data-title);
       position: absolute;
       top: 1px;
       left: 1px;
       width: calc(50% - 20px);
       padding: 5px 10px;
       white-space: nowrap;
       text-align: left;
       font-weight: bold;
   }
}

Hope this will help!!

```HTML
<!DOCTYPE html>
<html>
<head>
    <style type="text/css">

        table {
            width: 100%;
            text-align: left;
        }

        @media only screen and (max-width: 768px) {

            .table-responsive table,
            .table-responsive thead,
            .table-responsive tbody,
            .table-responsive tfoot,
            .table-responsive tr,
            .table-responsive th,
            .table-responsive td {
                display: block;
            }

            .table-responsive thead tr {
                position: absolute;
                top: -9999px;
                left: -9999px;
            }

            .table-responsive tfoot tr > th {
                position: absolute;
                top: -9999px;
                left: -9999px;
            }

            .table-responsive tr {
                border: 1px solid #ccc;
            }

            .table-responsive td {
                border: none;
                border-bottom: 1px solid #eee;
                position: relative;
                white-space: normal;
                text-align: left;
                padding: 5px 10px 5px calc(50% + 10px);
            }

            .table-responsive td:before {
                content: attr(data-title);
                position: absolute;
                top: 1px;
                left: 1px;
                width: calc(50% - 20px);
                padding: 5px 10px;
                white-space: nowrap;
                text-align: left;
                font-weight: bold;
            }
        }

    </style>
</head>
<body>


<div class="table-responsive">
    <table>
        <thead>
        <tr>
            <th>User ID</th>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Username</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td data-title="User ID">0001</td>
            <td data-title="First Name">Maria</td>
            <td data-title="Last Name">Anders</td>
            <td data-title="Username">@maria</td>
        </tr>
        <tr>
            <td data-title="User ID">0002</td>
            <td data-title="First Name">Christina</td>
            <td data-title="Last Name">Berglund</td>
            <td data-title="Username">@christina</td>
        </tr>
        <tr>
            <td data-title="User ID">0003</td>
            <td data-title="First Name">Francisco</td>
            <td data-title="Last Name">Chang</td>
            <td data-title="Username">@francisco</td>
        </tr>
        <tr>
            <td data-title="User ID">0004</td>
            <td data-title="First Name">Roland</td>
            <td data-title="Last Name">Mendel</td>
            <td data-title="Username">@roland</td>
        </tr>
        <tr>
            <td data-title="User ID">0005</td>
            <td data-title="First Name">Philip</td>
            <td data-title="Last Name">Cramer</td>
            <td data-title="Username">@philip</td>
        </tr>
        </tbody>
        <tfoot>
        <tr>
            <th colspan="3" align="right">Total User: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</th>
            <td data-title="Total User:">5</td>
        </tr>
        </tfoot>
    </table>
</div>

</body>
</html>
```

