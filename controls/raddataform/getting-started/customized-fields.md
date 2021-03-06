---
title: Customized Fields
page_title: Customized Fields
description: Customized Fields
slug: raddataform-customized-fields
tags: customized,fields
published: True
position: 2
---

# Customized Fields



## 

RadDataForm auto-generates its fields by default based on the properties of the source objects. They are stacked vertically in a standard form layout and depend on the type of each property.

![](images/RadDataForm_bindToCollection.png)

However, sometimes you may decide on customizing or totally changing them. In addition to displaying auto-generated fields, RadDataForm allows custom placement of the fields. Consequently, it may be designed to look like:

![](images/RadDataForm_customizedFields.png)



The key properties here are:

* ReadOnlyTemplate;

* NewItemTemplate;

* EditTemplate;

All of them are of type DataTemplate and there is no limitation on the types of controls you may place inside. Their DataContext will be the current item of the RadDataForm.

>Custom-defined fields may coexist with the auto-generated ones or the auto-generated may be canceled.

Once you set the AutoGeneratedFields property of the RadDataForm to "False", the implicit generation of the fields will be turned off:

#### __C#__

{{region raddataform-customized-fields_0}}

	this.DataForm1.AutoGenerateFields = false;
	{{endregion}}



#### __VB.NET__

{{region raddataform-customized-fields_1}}

	Me.DataForm1.AutoGenerateFields = False
	{{endregion}}



#### __XAML__

{{region raddataform-customized-fields_2}}

	<telerik:RadDataForm x:Name="DataForm1" AutoGenerateFields="False" />
	{{endregion}}



The three data templates - ReadOnlyTemplate, NewItemTemplate and EditTemplate - correspond to the relevant modes of the RadDataForm. So, when the form is in read-only mode, the ReadOnlyTemplate is displayed, when in edit-mode - the EditModeTemplate and when a new item is added - the NewItemTemplate.

Lets say you have defined this DataTemplate:

#### __XAML__

{{region raddataform-customized-fields_7}}

	<Grid.Resources>
	  <DataTemplate x:Key="MyTemplate">
	    <Grid>
	      <Grid.ColumnDefinitions>
	        <ColumnDefinition/>
	        <ColumnDefinition/>
	      </Grid.ColumnDefinitions>
	      <Grid.RowDefinitions>
	        <RowDefinition/>
	        <RowDefinition/>
	      </Grid.RowDefinitions>
	      <telerik:DataFormDataField Label="First Name" DataMemberBinding="{Binding FirstName, Mode=TwoWay}" />
	      <telerik:DataFormDataField Grid.Column="1" Label="Last Name" DataMemberBinding="{Binding LastName, Mode=TwoWay}" />
	      <telerik:DataFormCheckBoxField Grid.Column="1" Grid.Row="1" Label="Married" DataMemberBinding="{Binding IsMarried, Mode=TwoWay}" />
	    </Grid>
	  </DataTemplate>
	</Grid.Resources>
	{{endregion}}



Then you can assign the ReadOnlyTemplate like so:

#### __XAML__

{{region raddataform-customized-fields_3}}

	<Grid>
	 <telerik:RadDataForm x:Name="DataForm1"
	                           AutoGenerateFields="False" 
	                           ReadOnlyTemplate="{StaticResource MyTemplate}">
	 </telerik:RadDataForm>
	</Grid>
	{{endregion}}



The resultant view will be as follows:

![](images/RadDataForm_customizedFields.png)

Similarly you can assign the EditTemplate:

#### __XAML__

{{region raddataform-customized-fields_8}}

	<Grid>
	  <telerik:RadDataForm x:Name="DataForm1"
	                            AutoGenerateFields="False"
	                            EditTemplate="{StaticResource MyTemplate}">
	  </telerik:RadDataForm>
	</Grid>
	{{endregion}}



The resultant view will be as follows:

![](images/RadDataForm_autogeneratedFiels_EditMode.png)

For each different state, you will need to define another template. It could be with the same content or it could be with a different one.

>You will need to define separate templates for the read-only and edit modes.

On the other hand, if you make your mind on displaying quite different controls instead of the standard ones, you may place them in the data templates as well. For example, for editing number values, you may use the RadNumericUpDown control:

#### __XAML__

{{region raddataform-customized-fields_4}}

	<Grid>
	 <Grid.Resources>
	  <DataTemplate x:Key="MyTemplate">
	   <StackPanel Orientation="Horizontal" >
	    <TextBlock Text="Age" Width="20" Height="20" Foreground="Blue" Margin="0,0,10,0" />
	    <telerik:RadNumericUpDown Value="{Binding Age, Mode=TwoWay}" />
	   </StackPanel>
	  </DataTemplate>
	 </Grid.Resources>
	 <telerik:RadDataForm x:Name="DataForm1"
	                           AutoGenerateFields="False" 
	                           ReadOnlyTemplate="{StaticResource MyTemplate}">
	 </telerik:RadDataForm>
	</Grid>
	{{endregion}}



The result should be as follows:

![](images/RadDataForm_customizedFields_NewControls.png)

Furthermore, you may customize the data fields as well. For example, a regular DataFormDataField may be defined in a custom template and the default content may be replaced:{% if site.site_name == 'WPF' %}

#### __XAML__

{{region raddataform-customized-fields_5}}

	<Grid x:Name="LayoutRoot" Background="White">
	     <Grid.Resources>
	          <DataTemplate x:Key="MyTemplate">
	              <StackPanel Orientation="Horizontal" >
	                  <telerik:DataFormDataField>
	                      <StackPanel Orientation="Horizontal">
	                          <TextBox Text="{Binding Age,Mode=TwoWay}" Margin="0,0,10,0" />
	                          <TextBlock Text="years" Foreground="Green"  VerticalAlignment="Bottom" />
	                      </StackPanel>
	                  </telerik:DataFormDataField>
	               </StackPanel>
	          </DataTemplate>
	      </Grid.Resources>
	      <telerik:RadDataForm x:Name="DataForm1"
	                           AutoGenerateFields="False" 
	                           ReadOnlyTemplate="{StaticResource MyTemplate}">            
	    </telerik:RadDataForm>
	</Grid>
	{{endregion}}

{% endif %}{% if site.site_name == 'Silverlight' %}

#### __XAML__

{{region raddataform-customized-fields_6}}

	<Grid x:Name="LayoutRoot" Background="White">
	     <Grid.Resources>
	          <DataTemplate x:Key="MyTemplate">
	              <StackPanel Orientation="Horizontal" >
	                  <telerik:DataFormDataField>
	                       <telerik:DataFormDataField.ContentTemplate>
	                         <DataTemplate>
	                              <StackPanel Orientation="Horizontal">
	                                  <TextBox Text="{Binding Age,Mode=TwoWay}" Margin="0,0,10,0" />
	                                  <TextBlock Text="years" Foreground="Green"  VerticalAlignment="Bottom" />
	                              </StackPanel>
	                          </DataTemplate>
	                      </telerik:DataFormDataField.ContentTemplate>
	                  </telerik:DataFormDataField>
	               </StackPanel>
	          </DataTemplate>
	      </Grid.Resources>
	      <telerik:RadDataForm x:Name="DataForm1"
	                           AutoGenerateFields="False" 
	                           ReadOnlyTemplate="{StaticResource MyTemplate}">            
	    </telerik:RadDataForm>
	</Grid>
	{{endregion}}

{% endif %}

![](images/RadDataForm_customizedFields_NewContent.png)


