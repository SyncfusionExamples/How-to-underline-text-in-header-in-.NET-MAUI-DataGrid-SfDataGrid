# How to underline text in header in .NET MAUI DataGrid (SfDataGrid) ?
In this article, we will show you how to underline text in header in [.Net Maui DataGrid](https://www.syncfusion.com/maui-controls/maui-datagrid).

## Approach 1
You can define the style for the SfDataGridHeaderLabel in the ResourceDictionary.

**xaml**

The below code ensures that all header labels in the SfDataGrid will display their text underlined, providing a consistent and customized appearance.
```
 <ContentPage.BindingContext>
     <local:EmployeeViewModel x:Name="viewModel"/>
 </ContentPage.BindingContext>

 <ContentPage.Resources>
    <ResourceDictionary>
        <Style TargetType="syncfusion:SfDataGridHeaderLabel">
            <Setter Property="TextDecorations"
                    Value="Underline" />
        </Style>
    </ResourceDictionary>
</ContentPage.Resources>
``` 

## Approach 2
You can define a header template to customize the appearance of the column header using a DataTemplate.

**xaml**
```
<ContentPage.BindingContext>
    <local:EmployeeViewModel x:Name="viewModel" />
</ContentPage.BindingContext>

<syncfusion:SfDataGrid x:Name="sfGrid" 
                       GridLinesVisibility="Both"
                       AutoGenerateColumnsMode="None"
                       HeaderGridLinesVisibility="Both"
                       ColumnWidthMode="Auto"
                       ItemsSource="{Binding Employees}">

    <syncfusion:SfDataGrid.Columns>
        <syncfusion:DataGridNumericColumn MappingName="EmployeeID"
                                          Format="#">
            <syncfusion:DataGridNumericColumn.HeaderTemplate>
                <DataTemplate>
                    <Label Text="Employee ID" HorizontalOptions="Center" VerticalOptions="Center"
                           TextDecorations="Underline" />
                </DataTemplate>
            </syncfusion:DataGridNumericColumn.HeaderTemplate>
        </syncfusion:DataGridNumericColumn>
        <syncfusion:DataGridTextColumn MappingName="Name"
                                       HeaderText="Employee Name" />
        <syncfusion:DataGridTextColumn MappingName="Title"
                                       HeaderText="Designation" />
        <syncfusion:DataGridDateColumn MappingName="HireDate"
                                       HeaderText="Hire Date" />
    </syncfusion:SfDataGrid.Columns>

</syncfusion:SfDataGrid>
```

### Approach 3
You could achive this in the code behind with custom HeaderCellRenderer.

**C #**
```
public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
        sfGrid.CellRenderers.Remove("ColumnHeader");
        sfGrid.CellRenderers.Add("ColumnHeader", new DataGridHeaderCellRendererExt());
    }
}

public class DataGridHeaderCellRendererExt : DataGridHeaderCellRenderer
{
    protected override void OnInitializeDisplayView(DataColumnBase dataColumn, SfDataGridContentView? view)
    {
        base.OnInitializeDisplayView(dataColumn, view);

        if (view!.Content is Grid headerView)
        {
            var label = headerView.Children.FirstOrDefault(child => child is SfDataGridHeaderLabel);

            if (label != null && label is SfDataGridHeaderLabel newLabel)
            {
                newLabel.TextDecorations = TextDecorations.Underline;
            }
        }
    }
}
```

 ![Underline.png](https://support.syncfusion.com/kb/agent/attachment/inline?token=eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNobWFjLXNoYTI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjMzNDQzIiwib3JnaWQiOiIzIiwiaXNzIjoic3VwcG9ydC5zeW5jZnVzaW9uLmNvbSJ9.SYnyxDr6ZXun7erIL95WZeFPefx9y343iEpUFxI0mQc)

[View sample in GitHub](https://github.com/SyncfusionExamples/How-to-underline-text-in-header-in-.NET-MAUI-DataGrid-SfDataGrid)

Take a moment to explore this [documentation](https://help.syncfusion.com/maui/datagrid/overview), where you can find more information about Syncfusion .NET MAUI DataGrid (SfDataGrid) with code examples. Please refer to this [link](https://www.syncfusion.com/maui-controls/maui-datagrid) to learn about the essential features of Syncfusion .NET MAUI DataGrid (SfDataGrid).
 
##### Conclusion
 
I hope you enjoyed learning about how to underline text in header in .NET MAUI DataGrid (SfDataGrid).
 
You can refer to our [.NET MAUI DataGrid’s feature tour](https://www.syncfusion.com/maui-controls/maui-datagrid) page to learn about its other groundbreaking feature representations. You can also explore our [.NET MAUI DataGrid Documentation](https://help.syncfusion.com/maui/datagrid/getting-started) to understand how to present and manipulate data. 
For current customers, you can check out our .NET MAUI components on the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to explore our .NET MAUI DataGrid and other .NET MAUI components.
 
If you have any queries or require clarifications, please let us know in the comments below. You can also contact us through our [support forums](https://www.syncfusion.com/forums), [Direct-Trac](https://support.syncfusion.com/create) or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sfdatagrid), or the feedback portal. We are always happy to assist you!