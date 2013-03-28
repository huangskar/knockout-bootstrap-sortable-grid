Knockout pageable and sortable data table
=============================

###Basic
![Basic Example](https://raw.github.com/labory/knockout-bootstrap-sortable-data-table/master/assets/basic-example.png)
###View

    <table data-bind="dataTable: tableViewModel"><!-- --></table>

###ViewModel

    $(function () {
        var ExamplePageViewModel = function() {
            var self = this;
            self.getData = function (page, size, sortField, sortOrder, callback) {
                var params = "?page.page=" + (page) + "&page.size=" + size
                  + "&page.sort=" + sortField + "&page.sort.dir=" + sortOrder;
                $.getJSON("/frameworks" + params, callback);
            };
            self.tableViewModel = new ko.dataTable.ViewModel({
                columns: [
                    { name: "FRAMEWORK", value: "name", sortField: "name", width: "150px" },
                    { name: "LICENSE", value: "license", sortField: "license", width: "150px" },
                    { name: "DEPENDENCY", value: "dependency", sortField: "dependency", width: "150px" },
                    { name: "SIZE (Gzipped)", value: function (item) { return item.size != '' ? item.size + ' kb' : ''},
                      sortField: "size", width: "150px"}
                ],
                sortable: true,
                loader: self.getData,
                pageSize: 10
            });
        };
        ko.applyBindings(new ExamplePageViewModel());
    });
    
###Dependencies
  * Knockout
  * Jquery
  * bootstrap pagination css
