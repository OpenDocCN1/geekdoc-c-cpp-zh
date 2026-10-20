```
case "r":
	return Revenue.ToString();
case "p":
	return ContactPhone;
case "nr":
	return string.Format("{0,20}, {1,10:C}", Name, Revenue);
case "np":
	return string.Format("{0,20}, {1,15}", Name, ContactPhone);
case "pr":
	return string.Format("{0,15}, {1,10:C}", ContactPhone, Revenue);
case "pn":
	return string.Format("{0,15}, {1,20}", ContactPhone, Name);
case "rn":
	return string.Format("{0,10:C}, {1,20}", Revenue, Name);
case "rp":
	return string.Format("{0,10:C}, {1,20}", Revenue, ContactPhone);
case "nrp":
	return string.Format("{0,20}, {1,10:C}, {2,15}", Name, Revenue, ContactPhone);
case "npr":
	return string.Format("{0,20}, {1,15}, {2,10:C}", Name, ContactPhone, Revenue);
case "pnr":
	return string.Format("{0,15}, {1,20}, {2,10:C}", ContactPhone, Name, Revenue);
case "prn":
	return string.Format("{0,15}, {1,10:C}, {2,15}", ContactPhone, Revenue, Name);
case "rpn":
	return string.Format("{0,10:C}, {1,15}, {2,20}", Revenue, ContactPhone, Name);
case "rnp":
	return string.Format("{0,10:C}, {1,20}, {2,15}", Revenue, Name, ContactPhone);
```