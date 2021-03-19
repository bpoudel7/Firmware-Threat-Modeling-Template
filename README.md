# Firmware Threat Modeling Template
This repo includes templates that can be used while performing threat modeling using Microsoft Threat Modeling Tool. These templates are helpful if you are looking for a more firmware or hardware centric threat modeling using Microsoft Threat Modeling Tool (https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling).

# Entities or Elements of a Firmware Threat Model

## Modeling an API or Firmware Module
MS-TMT uses concept of Process to model a piece of code that perform one specific function. This templates follows the same trend. The firmware APIs or modules are modeled as Process.

### Process
Process can be a firmware module like a firmware update module, or an internal key management module, or an interrupt handling module, or a protocol parser module, or an API that performs a very specific function.

#### Attributes of a Process

| Attribute Name | Values | Description|
| :--------------| :------| :----------|
| **Code Type**  | Third Party Code | The API or module belongs to a third party library |
|                | Open Source Code | The API or module belongs to an open source library |
|                | Home Grown Code | The API or module is developed by your organization |
|                | Crypto Code | The API or module performs cryptographic operations like AES encryption, SHA3-256 Hashing, etc. |
|                | Key Management Code | The API or module performs internal key management in the device |
|                | User Credential Handling Code | The API or module takes user credential as input and perform computation on that data |
|                | Includes Mathamatical Computation Code | The API or module perform mathamatical computation |
| | | |
| **Origin** | Managed Code | The API or module is mainatined by your team |
|            | Foreign Code | The API or module is not maintained by your team |
| | | |
| **Language**| C | The API or module is written in C Programming Language |
|             | C++ | The API or module is written in C++ Programming Language |
|             | C/C++ | The API or module is written in mix of C and C++ Programming Language |
|             | Rust | The API or module is written in Rust Programming Language |
|             | Python | The API or module is written in Python Programming Language |
|             | Other | The API or module is written in some other Programming Language |
| | | |
| **Running with** | Kernel Privilege | Process is running in Kernel Mode |
|                  | Standard User with Elevation of Privilege | Process is running in user mode with a valid elevation of privilege |
|                  | Standard User without Elevation of Privilege | Process is running in strict user mode |
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
|                        | Not Applicable | The process does not take input  |
| | | |
| **Affected by** | HW or SW Interrupt | The process can be interrupted by a high priority interrupt routines |
|                 | HW Power Event | The process can be affected by unforeseen power events |
|                 | Aging | The process is affected by the aging of the hardware |
|                 | Eletromagnetic Disturbances | The process is sensitive to electromagnetic disturbances |
|                 | Extreme Temperature | The process is sensitive to huge temperature variation of environment |
|                 | Voltage Jitter | The process is affected by voltage glitches or voltage tampering |
|                 | Clock Jitter | The process is affected by clock glitch or clock signal tampering |
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
| | | |
| **Exception Handling Done** | Yes | Process perform some form of exception handling |
|                      | No | Process does not perform any exceptional handling |
|                      | Not Applicable |

## Modeling Storage
A firmware code running in a typical microcontroller uses a varieties of memories. A process running in a typical microcontroller uses stack memory section, heap memory section, various level of instruction and data cache, DRAM memory, flash memory, etc.

### Attributes of Data Storage

| Attribute Name | Values | Description|
| :--------------| :------| :----------|
| **Storage Type** | SRAM | SRAM Primary Memory. Stack and heap section lives in this memory. |
|                  | DRAM | DRAM Memory |
|                  | OTP eFuse | One-time programmable (OTP) memory is a type of non-volatile memory (NVM) that commonly comprises of electrical fuse (eFuse) and antifuse. In relation to security, antifuse is better than eFuse because there is no visible difference between a programmed bit and unprogrammed bit. |
|                  | NAND or Optane | Non-volatile memory |
|                  | SPI Flash | Flash memory |
|                  | ROM | PROM or EPROM or EEPROM or Mask ROM |
|                  | HW Key Cache | A dedicated memory to store runtime keys |
|                  | Registers | CPU registers |
|                  | Cache | Instruction or data cache |
| | | |
| **Stores User Data** | No | The memory does not store user data |
|                      | Yes | The memory stores user data |
|                      | Not Applicable |  |
| | | |
| **Stores Configuration Data** | No | The memory does not store configuration data |
|                               | Yes | The memory stores configuration data |
|                               | Not Applicable |  |
| | | |
| **Stores Vendor Data** | No | The memory does not store vendor data |
|                        | Yes | The memory stores vendor data |
|                        | Not Applicable |  |
| | | |
| **Stores Crypto Keys or Secrets** | No | The memory does not store secrets |
|                                   | Yes | The memory stores secrets |
|                                   | Not Applicable |  |
| | | |
| **Part of Secure Encalve or TEE** | No | The memory is not a part of secure hw enclave or trusted execution environment |
|                                   | Yes | The memory is a part of secure hw enclave or trusted execution environment |
|                                   | Not Applicable |  |
| | | |
| **Stores Log or Telemetry Data** | No | The memory does not store log or telemetry data |
|                                  | Yes | The memory stores log or telemetry data |
|                                  | Not Applicable |  |
| | | |
| **Stores Critical Security Parameters** | No | The memory does not store security critical data structures |
|                                         | Yes | The memory stores security critical data structures which if leaked has a significant security consequences |
|                                         | Not Applicable |  |
| | | |
| **Encrypted** | No | The data in the memory is not encrypted |
|               | Yes | The data in the memory is encrypted | |
|               | Not Applicable |  |
| | | |

| **Encrypted using Authenticated Encryption** | No | The data in memory is not encrypted using authenticated encryption scheme |
|                                              | Yes | The data in memory is encrypted using authenticated encryption scheme |
|                                              | Not Applicable |  |
| | | |

| **Signed** | No | The data in memory does not have digital signature to verify its authenticity |
|            | Yes | The data in memory have digital signature to verify its authenticity |
|            | Not Applicable |  |
| | | |
| **Read Only Access** | No | The memory can be read and write |
|                      | Yes | The memory is read only |
|                      | Not Applicable |  |
| | | |
| **Read-Write Access** | No | The memory does not have read-write access |
|                      | Yes | The memory can be read and written to |
|                      | Not Applicable |  |
| | | |

| **Backup** | No | The memory does not hold back up data |
|            | Yes | The memory content is a back up copy of some data |
|            | Not Applicable |  |
| | | |
| **Shared** | No | This is not a shared memory |
|            | Yes | This is a shared memory or memory section |
|            | Not Applicable |  |
| | | |
| **Stores Boot Code** | No | This memory does not store boot code |
|                      | Yes | This memory stores boot code |
|                      | Not Applicable |  |
| | | |
| **Stores Firmware Code** | No | This memory does not store firmware image |
|                          | Yes | This memory holds firmware image |
|                          | Not Applicable |  |
| | | |
| **Access Control Enforced** | No | This memory does not have access control mechanism |
|                             | Yes | The content of this memory has some form of access control mechanism |
|                             | Not Applicable |  |
| | | |
| **Stores Credentials** | No | This memory does not store credential data |
|                        | Yes | This memory stores credential data |
|                        | Not Applicable |  |
| | | |
