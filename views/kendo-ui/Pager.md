```js
var dataSource = new kendo.data.DataSource({
  data: [
    { productName: "Tea", category: "Beverages" },
    { productName: "Coffee", category: "Beverages" },
    { productName: "Ham", category: "Food" },
    { productName: "Bread", category: "Food" },
    { productName: "Tea", category: "Beverages" },
    { productName: "Coffee", category: "Beverages" },
    { productName: "Ham", category: "Food" },
    { productName: "Bread", category: "Food" },
    { productName: "Tea", category: "Beverages" },
    { productName: "Coffee", category: "Beverages" },
    { productName: "Ham", category: "Food" },
    { productName: "Bread", category: "Food" }
  ],
  pageSize: 1
});

$("#pager").kendoPager({
  dataSource: dataSource,
  messages: {
    empty: "No data", // 没有数据时显示的消息
    display: "Showing {0}-{1} from {2} data items", // （默认值：“{0} - {2} 个项目中的 {1} 个”）
    allPages: "See All",
    first: "First Page",
    previous: "Previous Page",
    next: "Next Page",
    last: "Last Page",
    refresh: "Refresh data"
    // numbersSelectLabel: "Select page number",
    // pageSizeDropDownLabel: "page size"
    // page: "Enter page",
    // pageButtonLabel: "This is page {0}"
  },
  pageSize: 5, //默认显示条数
  previousNext: true,
  pageSizes: false, //false 隐藏
  buttonCount: 5,
  input: false,
  numeric: true,
  selectTemplate:
    '<li class="k-link"><span style="color:red">#=text#</span></li>',
  linkTemplate:
    '<li><a href="\\#" class="k-link" data-#=ns#page="#=idx#"><strong>#=text#</strong></a></li>',
  refresh: true, //刷新按钮
  navigatable: true //键盘导航
});

dataSource.read();

```

