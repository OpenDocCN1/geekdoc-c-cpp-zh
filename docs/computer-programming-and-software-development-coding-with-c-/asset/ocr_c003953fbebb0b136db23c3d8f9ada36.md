```
<div class='row'>
  <div class='col-md-6'>
    <h4>Filtered by: </h4>
  </div>
</div>
<div class='table-responsive'>
  <table class='table'>
    <thead>
      <tr>
        <th>
          <button class='btn btn-primary'>
            Show Image
          </button>
        </th>
        <th>Product</th>
        <th>Code</th>
        <th>Available</th>
        <th>Price</th>
        <th>5 Star Rating</th>
      </tr>
    </thead>
    <tbody>

    </tbody>
  </table>
</div>
</div>
```

The first column header is a button to show the product image, and here is the table body. We definitely don't want to hard code in the products here, so let's leave the table body empty for now. So we have the start of a template defined for our component.

Remember the steps for building a component that we covered previously? We define a class, we add a Component decorator to define the metadata and specify the template, and we import what we need.