# Key Terms You Should Know

standard access list, wildcard mask

# Additional Practice for This Chapter’s Processes

For additional practice with analyzing subnets, you may do the same set of practice problems using your choice of tools:

+   - **Application:** Use the Basic IPv4 Access Control Lists application on the DVD or companion website.
+   - **PDF:** Alternatively, practice the same problems found in these apps using DVD Appendix D, “Practice for Chapter 16: Basic IPv4 Access Control Lists.”

# Command References

Tables 16-6 and 16-7 list configuration and verification commands used in this chapter. As an easy review exercise, cover the left column in a table, read the right column, and try to recall the command without looking. Then repeat the exercise, covering the right column, and try to recall what the command does.

**Table 16-6 — Chapter 16 Configuration Command Reference**

| Command | Description |
|---|---|
| `access-list access-list-number {deny \| permit} source [source-wildcard] [log]` | Global command for standard numbered access lists. Use a number between 1 and 99 or 1300 and 1999, inclusive. |
| `access-list access-list-number remark text` | Defines a remark that helps you remember what the ACL is supposed to do. |
| `ip access-group number {in \| out}` | Interface subcommand to enable access lists. |

**Table 16-7 — Chapter 16 EXEC Command Reference**

| Command | Description |
|---|---|
| `show ip interface [type number]` | Includes a reference to the access lists enabled on the interface. |
| `show access-lists [access-list-number \| access-list-name]` | Shows details of configured access lists for all protocols. |
| `show ip access-lists [access-list-number \| access-list-name]` | Shows IP access lists. |