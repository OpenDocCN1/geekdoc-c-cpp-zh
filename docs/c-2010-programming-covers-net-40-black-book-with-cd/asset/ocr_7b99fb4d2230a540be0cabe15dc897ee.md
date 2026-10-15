```
Font-Bold="True" Font-Size="0.8em"
ForeColor="#333333" /> <ZoneTemplate>
<asp:BehaviorEditorPart
ID="BehaviorEditorPart1" runat="server" />
<asp:LayoutEditorPart
ID="LayoutEditorPart1" runat="server"  />
</ZoneTemplate>
<HeaderVerbStyle Font-Bold="False"
Font-Size="0.8em" Font-Underline="False"
ForeColor="#333333" />
<PartChromeStyle
BorderColor="#E2DED6" BorderStyle="Solid" BorderWidth="1px" />
<PartStyle
BorderColor="#F7F6F3" BorderWidth="5px" />
<FooterStyle BackColor="#E2DED6"
HorizontalAlign="Right" />
<EditUIStyle Font-Names="Verdana"
Font-Size="0.8em" ForeColor="#333333" />
<InstructionTextStyle
Font-Size="0.8em" ForeColor="#333333" />
<ErrorStyle Font-Size="0.8em" />
<VerbStyle Font-Names="verdana"
Font-Size="0.8em" ForeColor="#333333" />
<EmptyZoneTextStyle
Font-Size="0.8em" ForeColor="#333333" />
<PartTitleStyle Font-Bold="True"
Font-Size="0.8em" ForeColor="#333333" />
</asp:EditorZone>
<br /><br /><br />
</div>
</form>
</body>
</html>
```

4. Now, add the following code inside the <system.web> section of the Web.config file:

```
<webParts>
<personalization>
<authorization>
<allow users="*" verbs="entersharedscope"/>
</authorization>
</personalization>
</webParts>
```

5. To run the CustomWebPart Web application, press the F5 key. Figure 16.52 shows the output:

![](bbox=[0.2, 0.67, 0.75, 0.92])

Figure 16.52: The Output of CustomWebPart Web Application