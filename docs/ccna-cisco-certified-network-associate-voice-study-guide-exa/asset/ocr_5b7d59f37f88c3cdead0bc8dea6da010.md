Now that the gateway is configured to use the gatekeeper, a single dial peer must be created to indicate that the gatekeeper should be used for all four-digit extensions. The dial-peer commands in the preceding example perform this operation. Notice, specifically, the session target ras command, which indicates that a gatekeeper (which is a RAS server) should be used for all four-digit extensions.

# Verifying Gatekeeper Configuration

After the gateways have been configured to use the gatekeeper, as explained in the preceding section, the gatekeeper operations can be verified. Several show commands are useful for verification, including:

+   - **show gatekeeper status** — This command displays the gatekeeper state, the zone name, whether accounting is enabled or disabled, security features, and the bandwidth limits and utilization.
+   - **show gatekeeper calls** — This command shows all calls currently in progress that were established through the gatekeeper.
+   - **show gatekeeper endpoints** — Interestingly, this command shows the gateways because they are considered endpoints by the H.323 standard. It’s important to remember that this command is not limited to showing IP phones.
+   - **show gatekeeper zone** — This command displays the zone configuration information, including prefixes and subnets.

> > **Exam Watch**
> >
> > Be sure to know which show commands do what in relation to gatekeeper configuration and operation verification. They are very likely to show up on the CVOICE exam.