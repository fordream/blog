Title: Major Difference between MVVM and MVC
Date:2015-08-08
Category: 前端

In MVC, ***C*** (controller) must ***hard refereces*** a variable's name of UI elements from View. Therefore, changes in View will ***domino*** ***C*** code changes.

In MVVM, because of ***Data Binding*** mechanism, ***C*** (controller, or ViewModel) don't hard references a variable's name of UI elements from View. You can easily config data bindings in XAML/WPF. So, changes in View will not domino ***C*** code changes.




