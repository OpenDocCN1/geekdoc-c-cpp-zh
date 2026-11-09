+   2. Open the Code Editor window, then locate the code template for the btnSave control's Click event procedure. Before saving the phone number to the sequential access file, the procedure will replace the hyphens with the empty string. Click the **blank line** below the ' remove the hyphens comment. Type **strPhone = txtPhone.text.replace(“-”, string.empty)** and press **Enter**.
+   3. Save the solution, then start the application. First, enter an invalid phone number. Type **111-2222** as the phone number, then click the **Save** button. A message box opens and displays the “Invalid phone number” message. Close the message box.
+   4. Type **111-222-3333** as the phone number, then click the **Save** button. Type **222-333-4444** as the phone number, then click the **Save** button. Click the **Display** button. The button's Click event procedure reads each phone number from the phoneNumbers.txt file and displays each in the lblFileContents control. See Figure 24-6. Notice that the phone numbers do not contain any hyphens.

![](bbox=[0.06, 0.47, 0.94, 0.68])

Figure 24-6: Contents of the phoneNumbers.txt file displayed in the lblFileContents control

+   5. Click the **Exit** button.

In addition to displaying the phone numbers contained in the file, the Display button also should insert the appropriate hyphens in each number and then display the formatted number in the lblFormattedNumbers control. You can insert the hyphens using the Insert method, as shown in Figure 24-7.