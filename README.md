# ThreatModelingTemplate
This repo includes templates that can be used while performing threat modeling using Microsoft Threat Modeling Tool. These templates are helpful if you are looking for a more firmware or hardware centric threat modeling using Microsoft Threat Modeling Tool (https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling).

# Entities or Elements of Threat Model

## Process
Process can be a firmware module like firmware update module, or internal key management module, or interrupt handling module, protocol parser module, or an API that performs a very specific function.
### Attributes of a Process
| Attribute Name | Values | Description|
| :--------------| :------| :----------|
|                | Third Party Library | The API or module belongs to a third party library |
|                | Open Source Library | The API or module belongs to an open source library |
| **Code Type**  | Home Grown | The API or module is developed by your organization |
|                | Crypto Code | The API or module performs cryptographic operations like AES encryption, SHA3-256 Hashing, etc. |
|                | Key Management Code | The API or module performs internal key management in the device |
|                | User Credential Handling Code | The API or module takes user credential as input and perform computation on that data |
| | | |
| **Origin** | Managed Code | The API or module is mainatined by your team |
|            | Foreign Code | The API or module is not maintained by your team |
