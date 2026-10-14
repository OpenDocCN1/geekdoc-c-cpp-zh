# The Default.aspx file

```
<p>
    <asp:UpdatePanel ID="ShoutBoxPanel2" runat="server" UpdateMode="Conditional">
        <ContentTemplate>
            <p class="label">Name:</p>
            <p class="entry">
                <asp:TextBox ID="txtUserName" runat="server" MaxLength="15" Width="100px"></asp:TextBox>
                <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ErrorMessage="Name is required." ControlToValidate="txtUserName" Display="Dynamic" CssClass="error">
                </asp:RequiredFieldValidator>
            </p>
            <p class="label">Shout:</p>
            <p class="entry">
                <asp:TextBox ID="txtShout" runat="server" MaxLength="255" Width="220px"></asp:TextBox>
                <asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ErrorMessage="Shout is required." ControlToValidate="txtShout" Display="Dynamic" CssClass="error">
                </asp:RequiredFieldValidator>
            </p>
            <asp:Button ID="btnAddShout" runat="server" Text="Add Shout" />
            <asp:UpdateProgress ID="UpdateProgress1" runat="server" DynamicLayout="False">
                <ProgressTemplate>
                    <img src="Images/spinner.gif" alt="Please Wait" />
                    Uploading Comment...
                </ProgressTemplate>
            </asp:UpdateProgress>
        </ContentTemplate>
    </asp:UpdatePanel>
</p>
    </div>
    </div>
</div>
</form>
</body>
</html>
```