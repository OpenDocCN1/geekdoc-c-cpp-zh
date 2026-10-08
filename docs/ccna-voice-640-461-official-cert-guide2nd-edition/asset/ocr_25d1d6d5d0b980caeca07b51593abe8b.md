# Example 6-25 Creating Outgoing COR Lists

```
Router(config)#dial-peer cor list 911-CALL
Router(config)-dp-corlist)#member 911
Router(config)-dp-corlist)#exit
Router(config)#dial-peer cor list LOCAL-CALL
Router(config)-dp-corlist)#member LOCAL
Router(config)-dp-corlist)#exit
Router(config)#dial-peer cor list LD-CALL
Router(config)-dp-corlist)#member LD
Router(config)-dp-corlist)#exit
```

We eventually apply the COR lists shown in Example 6-25 as outgoing COR lists to the PSTN dial peers. If you were to read these COR lists in plain English, the 911-COR list would say, "For this COR list to allow the call, the caller must be assigned the 911 tag." The LOCAL-CALL COR list would say, "For this COR list to allow the call, the caller must be assigned the LOCAL tag." Hopefully, you get the idea, but keep in mind that the COR lists are not doing anything, because we have not yet applied them to the dial peers. Next, we create incoming COR lists, as shown in Example 6-26.

# Example 6-26 Incoming COR Lists

```
Router(config)#dial-peer cor list 911-ONLY
Router(config)-dp-corlist)#member 911
Router(config)-dp-corlist)#exit
Router(config)#dial-peer cor list 911-LOCAL
Router(config)-dp-corlist)#member 911
Router(config)-dp-corlist)#member LOCAL
Router(config)-dp-corlist)#exit
Router(config)#dial-peer cor list 911-LOCAL-LD
Router(config)-dp-corlist)#member 911
Router(config)-dp-corlist)#member LOCAL
Router(config)-dp-corlist)#member LD
Router(config)-dp-corlist)#exit
```

We eventually apply the COR lists shown in Example 6-26 to the ephone-ds to grant calling privileges. If you were to read these COR lists in plain English, the 911-ONLY COR list would say, "Anyone assigned to this COR list can call dial peers requiring the 911 tag." The 911-LOCAL COR list would say, "Anyone assigned to this COR list can call dial peers requiring the 911 or LOCAL tags."

**Note:** You might wonder, "How do these COR lists say different things when they're created the same way?" Great question! This is what makes COR lists so confusing. Both inbound and outbound COR lists are created the same way. The effect they have is completely based on how you apply them. If you apply a COR list in the outbound direction, it says, "I will require a caller to have the defined tags to complete a call." If you