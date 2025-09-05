# hide-checkbox-treeview-xamarin
How to conditionally hide the checkbox in Xamarin.Forms TreeView (SfTreeView)

**[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12142/how-to-conditionally-hide-the-checkbox-in-xamarin-forms-treeview-sftreeview)**

## Sample

### XAML
Bind the SfCheckBox.IsVisible property with TreeViewNode.Level and define converter to handle the Visibility.
```xaml
<treeView:SfTreeView x:Name="treeView"
                    ItemTemplateContextType="Node"
                    CheckBoxMode="Recursive" 
                    AutoExpandMode="RootNodesExpanded"
                    CheckedItems="{Binding CheckedItems}"
                    ItemsSource="{Binding Folders}">
    <treeView:SfTreeView.HierarchyPropertyDescriptors>
        <treeViewEngine:HierarchyPropertyDescriptor TargetType="{x:Type local:Folder}" ChildPropertyName="SubFolder"/>
        <treeViewEngine:HierarchyPropertyDescriptor TargetType="{x:Type local:SubFolder}" ChildPropertyName="Files"/>
        <treeViewEngine:HierarchyPropertyDescriptor TargetType="{x:Type local:File}" ChildPropertyName="SubFiles"/>
    </treeView:SfTreeView.HierarchyPropertyDescriptors>
 
    <treeView:SfTreeView.ItemTemplate>
        <DataTemplate>
            <Grid Padding="5">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="40"/>
                    <ColumnDefinition Width="*"/>
                </Grid.ColumnDefinitions>
                <checkBox:SfCheckBox x:Name="CheckBox" IsChecked="{Binding IsChecked, Mode=TwoWay}" CornerRadius="2" IsVisible="{Binding Level, Converter={StaticResource checkBoxVisibilityConverter}}"/>
                <Label Text="{Binding Content.FileName}" VerticalOptions="CenterAndExpand" HorizontalOptions="StartAndExpand" Grid.Column="1"/>
            </Grid>
        </DataTemplate>
    </treeView:SfTreeView.ItemTemplate>
</treeView:SfTreeView>
```

### Converter
```csharp
public class CheckBoxVisibilityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return (int)value == 0 ? false : true;
    }
}
```

## Requirements to run the demo
Visual Studio 2017 or Visual Studio for Mac.
Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.

## Conclusion

I hope you enjoyed learning about how to conditionally hide the checkbox in Xamarin.Forms TreeView (SfTreeView).

You can refer to our Xamarin.Forms TreeViewfeature tour page to know about its other groundbreaking feature representations and documentation, and how to quickly get started for configuration specifications.

For current customers, you can check out our components from the License and Downloads page. If you are new to Syncfusion, you can try our 30-day free trial to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our support forums, Direct-Trac, or feedback portal. We are always happy to assist you!