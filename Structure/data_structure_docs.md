# Roaming-Tool Data Structure Documentation

All data can be provided as a .json file or as JSON data through an API.

The following key words are reserved and shoult not be used.

- RT_MOBILE: Sets the value to the same as defined for calls to a mobile connection; only for outbound calls to a landline
- RT_UNDEFINED: Sets the value to the text, for undefined values (e.g. "No prices available")
- RT_TARFIF: Type needs to be set to register a definition as a tariff instead of a zone.

## **Country Data**

The following fields are avaiable.

### **name**

---

**Type:** string

**Mandatory:** true

**Example Value(s):** Germany

Name of the country.

### **zone**

---

**Type:** string

**Mandatory:** true

**Example Value(s):** ZONE_1, WORLD

Identifier of the default zone. This will be used if no other specific zone was found. If this zone is an empty string and no other information is avaiable, it will show the empty price text, defined in the [settings]().

### **isHome**

---

**Type:** boolean

**Mandatory:** false

**Example Value(s):** true / false

Identifies the country as the users home country. If this country is then selected as the users location, it will not be treated as roaming, but rather as an international call

### **inZone**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** IN_ZONE_1, IN_WORLD

Alternative zone for prices for inbound calls, that should be used if it differs from the default zone.

### **outZone**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** OUT_ZONE_1, OUT_WORLD

Alternative zone for prices for outbound calls, that should be used if it differs from the default zone.

### **smsZone**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** SMS_ZONE_1, SMS_WORLD

Alternative zone for SMS prices, that should be used if it differs from the default zone.

### **mmsZone**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** MMS_ZONE_1, MMS_WORLD

Alternative zone for MMS prices, that should be used if it differs from the default zone.

### **dataZone**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** DATA_ZONE_1, DATA_WORLD

Alternative zone for data prices, that should be used if it differs from the default zone.

### **comments**

---

**Type:** \[{"content": string, "displayType": string}]

**Mandatory:** false

**Example Value(s):** \[{"content": "No data roaming avaiable.", "displayType": "TARGET"}]

Define comments that should be displayed depending on the display type. You can define multiple comments for different conditions. A display type can be one of the following values:

**ALWAYS:** Will display the comment, regardless this country is used as a user location or target location.

**USER:** Will display the comment if the country is selected as the users location.

**TARGET:** Will display the comment if the country is selected as the targets location.

### **altCountry**

---

**Type:** string

**Mandatory:** false

**Example Value(s):** Portugal

Setting this field will get the prices based on the provided alternative country. If you use this, you can have the zone field be an empty string. This option is meant to be used for country or places that belong to a different one. E.g.: Madeira would define Portugal as an altCountry.

### **partners**

---

**Type:** \[string]

**Mandatory:** false

**Example Value(s):** ["Unnamed Carrier 1"]

A list of partner carriers, that will be shown if the country was selected as the users location.

## **Zone Data**

The following fields are avaiable.

### **zoneID**

---

**Type:** string

**Mandatory:** true

**Value for:** User Location

**Example Value(s):** DATA_ZONE_1, DATA_WORLD

The unique identifier of the zone.

### **inCalls**

---

**Type:** string

**Mandatory:** false

**Value for:** User Location

**Example Value(s):** free, 0,06€/Min.

The price of inbound calls.

### **outCallsMobileDefault**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/Min.

The price of outbound calls to a mobile phone. If not given, all outbound definitions need to have an outCallsMobile field.

### **outCallsLandDefault**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/Min., RT_MOBILE

The price of outbound calls to a landline. If not given, all outbound definitions need to have an outCallsMobile field. Will be the same as outCallsMobileDefault if set to RT_MOBILE.

### **inSMS**

---

**Type:** string

**Mandatory:** true

**Value for:** User Location

**Example Value(s):** free, 0,06€/SMS

The price of incoming SMS.

### **inMMS**

---

**Type:** string

**Mandatory:** true

**Value for:** User Location

**Example Value(s):** free, 0,36€/MMS

The price of incoming SMS.

### **outSMSDefault**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/SMS

The default price of outgoing SMS. If not given, all outbound definitions need to have an outSMS field.

### **outMMSDefault**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,36€/SMS

The default price of outgoing MMS. If not given, all outbound definitions need to have an outMMS field.

### **data**

---

**Type:** string

**Mandatory:** true

**Value for:** User Location

**Example Value(s):** free, 0,08€/50kb

The price of outgoing MMS.

### **callMailbox**

---

**Type:** string

**Mandatory:** false

**Value for:** User Location

**Example Value(s):** free, 0,08€/Min.

The price of for connections to the mailbox. Will be the price for a connection to the home country of the user, if not given.

### **zoneID of target zone or special tariff**

---

**Type:** "zoneID of target zone": {"outCallsMobile"?: string, "outCallsLand"?: string, "outSMS"?: string, "outMMS"?: string, "tariffs" : string}

**Mandatory:** false

**Value for:** Target Locations

**Example Value(s):** "EUROPE": {}, "WORLD": {"outCallsMobile": "1,45 €/Min.", "outCallsLand": "RT_MOBILE"}

Holds the prices for services to the targeted location. Use the zoneID of the target zone as an identifier.If a target zone is not defined, no values will be displayed. If a target zone is defined as an empty object, the default values (ending with Default) will be used.

### **type**

---

**Type:** string

**Mandatory:** false

**Value for:** Target and User Location

**Example Value(s):** RT_TARIFF

Defines wether this zone will be registred as a tariff and displayed as a selection option. If this field is set, displayName also needs to be defined. A tariff will only be avaiable if the base zone defines it in the tariffs property.

### **displayName**

---

**Type:** string

**Mandatory:** false

**Value for:** Input Controls

**Example Value(s):** Carriers Roaming Choice, Travel Package

If given for a tariff, this will be used as the name displayed next to the radio button.

### **bookingPrice**

---

**Type:** string

**Mandatory:** false

**Value for:** Tariff

**Example Value(s):** 4,99€, 2,55€/Month

Shows the price, that this tariff will cost. Only needed for tariffs.

### **isEURoaming**

---

**Type:** boolean

**Mandatory:** false

**Value for:** User Location

**Example Value(s):** true / false

Defines wether this zone falls under the EU regulations for roaming. Set this to true if the users home country belongs to the EU and this zone is meant for other EU countries. If this field ist set to true, it will show a EU flag as an additional hint.

### **zoneComments**

---

**Type:** \[{"content": string, "displayType": string}]

**Mandatory:** false

**Value for:** As per definition

**Example Value(s):** \[{"content": "No data roaming avaiable.", "displayType": "TARGET"}]

Define comments that should be displayed depending on the display type. You can define multiple comments for different conditions. A display type can be one of the following values:

**ALWAYS:** Will display the comment, regardless this zone is used as a user location or target location.

**USER:** Will display the comment if the zone is selected as the users location.

**TARGET:** Will display the comment if the zone is selected as the targets location.

### **outCallsMobile**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/Min.

The price of outbound calls to a mobile phone. If not given, the field outCallsMobileDefault needs to be given. If both fields are given, outCallsMobile will takes precedence over outCallsMobileDefault.

### **outCallsLand**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/Min., RT_MOBILE

The price of outbound calls to a landline. If not given, the field outCallsLandDefault needs to be given. If both fields are given, outCallsLand will takes precedence over outCallsLandDefault. Will be the same as outCallsMobile if set to RT_MOBILE.

### **outSMS**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,06€/SMS

The price of outgoing SMS. If not given, the field outSMSDefault needs to be given. If both fields are given, outSMS will takes precedence over outSMSDefault.

### **outMMS**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** free, 0,36€/SMS

The price of outgoing MMS. If not given, the field outMMSDefault needs to be given. If both fields are given, outMMS will takes precedence over outMMSDefault.

### **altZone**

---

**Type:** string

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** ZONE_1, WORLD

If this field is set, the same prices apply, that are defined in the given alternative target zone. Use this to prevent repettion of the same code

### **tariffs**

---

**Type:** \[string]

**Mandatory:** false

**Value for:** Target Location

**Example Value(s):** ZONE_1_TARIFF, WORLD_TARIFF

Set this field to link to a specific tariff. The given tariff must be defined in the same way as a zone. This field will be looked at, if the user can book additional products to lower the costs. The selecti
