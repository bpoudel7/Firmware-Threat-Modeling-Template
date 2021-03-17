# ThreatModelingTemplate
This repo includes templates that can be used while performing threat modeling using Microsoft Threat Modeling Tool. These templates are helpful if you are looking for a more firmware or hardware centric threat modeling using Microsoft Threat Modeling Tool (https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling).

# Entities or Elements of Threat Model

## Process
Process can be a firmware module like firmware update module, or internal key management module, or interrupt handling module, protocol parser module, or an API that performs a very specific function.
### Attributes of a Process
| Attribute Name | Values | Description|
| :--------------| :------| :----------|
| **Code Type**  | Third Party Code | The API or module belongs to a third party library |
|                | Open Source Code | The API or module belongs to an open source library |
|                | Home Grown Code | The API or module is developed by your organization |
|                | Crypto Code | The API or module performs cryptographic operations like AES encryption, SHA3-256 Hashing, etc. |
|                | Key Management Code | The API or module performs internal key management in the device |
|                | User Credential Handling Code | The API or module takes user credential as input and perform computation on that data |
| | | |
| **Origin** | Managed Code | The API or module is mainatined by your team |
|            | Foreign Code | The API or module is not maintained by your team |
| | | |
| **Running with** | Kernel Privilege | Process is running in Kernel Mode |
|                  | Standard User with Elevation of Privilege | Process is running in user mode with a valid elevation of privilege |
|                  | Standard User without Elevation fo Privilege | Process is running in strict user mode |
| | | |
| **Isolation Level** | Has Separate Runtime Context | The process has its own runtime context i.e., stack, heap, registers, code section, and data section |
|                     | Has Separate Stack and Heap Memory | The process has a dedicated stack and heap memory |
|                     | Runs in Secure Enclave or is a part of TEE | The process runs as a part of secure enclave or is a part of the trusted execution environment |
|                     | Shares Runtime Context | The process shares its runtime context with other processes |
| | | |
| **Accepts Input from** | External User or Entity | Process accepts input from host application or some other form of interaction with external user |
|                        | Remote User or Entity | Process accepts input from a remote user like remote firmware attestation tool or over-the-air firmware update tool, etc |
|                        | Another Process | Process accepts input from another process | 
|                        | GPIO Pins | Process accepts inputs from general purpose input pins |
|                        | Debug Port | Process accepts inputs from debug port like JTAG or UART |
|                        | Interrupt Source | Process accepts interrupt from hardware or software interrupt source |
|                        | Hardware Power Event | Process is affected by change in state of hardware power event like platform reset or platform powercycle |
|                        | Not Applicable | The process does not take input from  |
| | | |
| **Sanitizes Input** | Yes | Process perform some form of input validation before consuming the input data |
|                     | No | Process consumes the input data without any input validation |
|                     | Not Applicable |
| | | |
| **Sanitizes Output** | Yes | Process perform some form of output validation before returning the output data |
|                      | No | Process returns the output data without any output validation |
|                      | Not Applicable |
| | | |
| **Implements or Uses an Authentication Mechanism** | Yes | Process perform some form of output validation before returning the output data. Entity authentication can be a very basic operation like checking module ID or checking possession of some kind of token or checking password. More, authentication can involve challenge-response protocol based interaction or ZKP based interaction or digital certificates (or certificate chain) verification |
|                      | No | Process does not perform any form of entity authentication before communicating with another process |
|                      | Not Applicable |
| | | |
| **Implements or Uses an Authorization Mechanism** | Yes | Process perform some form of access control list check. Authorization can be achived by implementing access control mechanism or a ticket or a token based system |
|                      | No | Process does not perform any form of entity authorization before communicating with another process |
|                      | Not Applicable |
| | | |
| **Saves and Restores State or Context** | Yes | Process saves runtime context in NVM and restores later |
|                      | No | Process does not save-restore runtime context |
|                      | Not Applicable |
| | | |
| **Handles User Credentials** | Yes | Process perform some form of computation on user supplied credential like password |
|                      | No | Process does not handle user credential |
|                      | Not Applicable |

## External Interactor



