**on the Job**

To learn more about analog port configurations and options, visit the Cisco.com web site at http://www.cisco.com/en/US/docs/ios/voice/voiceport/configuration/guide/vo_cfg_analog_vps_ps6441_TSD_Products_Configuration_Guide_Chapter.html.

Depending on the router model, you will use different commands in global configuration mode to gain access to the voice port. On some models, you will use the *voice-port port* command. On others, you may use the *voice-port slot/port* command. On still others, you may use the *voice-port slot/subunit/port* command. Once you have entered *voice-port* configuration mode, you can configure the signaling type, tone signaling sounds, dialing type, ring frequency, ring number, ring cadence, and description. Some configuration options are available only on FXS ports, and these include ring frequency, ring number, and ring cadence. The dialing type is only available on FXO ports.

# ## Understanding Digital Ports

Digital ports come in two primary forms: T1/E1 and ISDN. The T1 lines can have up to 24 channels, with 23 channels usable for voice communications. The E1 lines can have up to 32 channels, with 30 channels usable for voice communications. The total data rate for a full T1 line is 1.544 Mbps with a bandwidth of 1.536 Mbps, and it is 2.048 Mbps with 1.984 Mbps in bandwidth for a full E1 line. Each channel contains 64 Kbps of bandwidth.

On digital circuits or ports, time division multiplexing (TDM) may be used. A TDM model uses time slices for specific channels, and the communication channels take turns and communicate only during their assigned time slice. The time is divided between the needed channels in order to multiplex (combine) multiple signals on the line. On a T1 line, 24 different slices or channels are provided, assuming a full T1 is purchased.

Statistical TDM reserves timeslots on the wire only when the slot is needed for data transmission. Statistical TDM allows for oversubscribing on the circuit, while traditional TDM does not allow for this feature. Statistical TDM is also known as packet-mode multiplexing.

**exam watch**

Remember that statistical TDM can be oversubscribed, while traditional TDM cannot. Traditional TDM uses assigned timeslots for channels, and the assignments do not change. Statistical TDM requests a timeslot only when it is needed.