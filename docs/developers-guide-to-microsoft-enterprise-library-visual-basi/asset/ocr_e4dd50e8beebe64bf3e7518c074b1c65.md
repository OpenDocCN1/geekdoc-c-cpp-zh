```
<EntLibValidators:PropertyProxyValidator id="firstNameValidator"
runa="server" ControlToValidate="FirstNameTextBox"
PropertyName="FirstName" RulesetName="RuleSetA"
SourceTypeName="ValidationQuickStart.BusinessEntities.Customer" />
```

One to be aware of is that, unlike the ASP.NET validation controls, the Validation block **PropertyProxyValidator** control does not perform client-side validation. However, it does integrate with the server-based code and will display validation error messages in the page in the same way as the ASP.NET validation controls.

For more information about ASP.NET integration, see the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.

# Windows Forms User Interface Validation

The validation block includes the **ValidationProvider** component that extends Windows Forms controls to provide validation using a rule set defined in your application through configuration, attributes, and self-validation. You can handle the **Validating** event to perform validation, or invoke validation by calling the **PerformValidation** method of the control. You can also specify an **ErrorProvider** that will receive formatted validation error messages.

To use the **ValidationProvider**, you add the assembly named Microsoft.Practices.EnterpriseLibrary.Validation.Integration.WinForms to your application, and reference it in your project.

For more information about Windows Forms integration, see the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.

# WPF User Interface Validation

The Validation block includes the **ValidatorRule** component that you can use in the binding of a WPF control to provide validation using a rule set defined in your application through configuration, attributes, and self-validation. To use the **ValidatorRule**, you add the assembly named Microsoft.Practices.EnterpriseLibrary.Validation.Integration.WPF to your application, and reference it in your project.

As an example, you can add a validation rule directly to a control, as shown here.

```
<TextBox x:Name="TextBox1">
    <TextBox.Text>
        <Binding Path="ValidatedStringProperty" UpdateSourceTrigger="PropertyChanged">
            <Binding.ValidationRules>
                <vab:ValidatorRule SourceType="{x:Type test:ValidatedObject}" SourcePropertyName="ValidatedStringProperty"/>
            </Binding.ValidationRules>
        </Binding>
    </TextBox.Text>
</TextBox>
```