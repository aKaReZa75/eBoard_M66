This comprehensive tree structure provides a complete reference for GSM/GPRS module AT commands organized by functionality. From basic communication and SIM card management to advanced features like MQTT messaging, this guide covers all essential commands for IoT and embedded projects. Each command includes a brief description to help developers quickly understand its purpose and implementation. Whether you're working with SMS, voice calls, internet connectivity, or remote data transmission, this reference serves as your go-to resource for GSM module integration.

```plaintext
 GSM/GPRS AT Commands
   ├── Basic Communication
   │   ├── AT                     - Test command to check communication
   │   ├── ATE0                   - Turn off command echo
   │   ├── AT+CMEE=2              - Enable verbose error messages
   │   └── AT+IPR=115200          - Set fixed UART baud rate to 115200 bps
   │   
   ├── SIM Card & Network
   │   ├── AT+CPIN?               - Check SIM card status
   │   ├── AT+CPIN="PIN"          - Enter SIM PIN code
   │   ├── AT+CSQ                 - Get signal quality
   │   ├── AT+CREG?               - Check network registration status
   │   └── AT+COPS?               - Get current operator
   │   
   ├── Module Configuration
   │   ├── AT+CFUN=1              - Set full functionality mode
   │   ├── AT+CFUN=0              - Minimum functionality (RF off)
   │   ├── AT+CFUN=4              - Airplane mode
   │   └── AT&W                   - Save current settings
   │
   ├── Voice Call Operations
   │   ├── AT+CLIP=1              - Enable caller ID display
   │   ├── ATD+number<number>;    - Dial voice call
   │   ├── ATA                    - Answer an incoming call
   │   ├── ATH                    - Hang up an ongoing call
   │   └── AT+CLCC                - List current calls
   │   
   ├── SMS Operations
   │   ├── SMS Configuration
   │   │   ├── AT+CMGF=1          - Set SMS mode to text
   │   │   ├── AT+CSCS="GSM"      - Set character set to GSM
   │   │   ├── AT+CSMP=17,167,0,0 - SMS text mode parameters (MCI, MTN)
   │   │   └── AT+CSMP=17,167,0,4 - SMS text mode parameters (Rightel)
   │   ├── SMS Management
   │   │   ├── AT+CMTI            - Incoming SMS indication   
   │   │   ├── AT+CMGR=<index>    - Read SMS by index from memory
   │   │   ├── AT+CMGL="ALL"      - List all SMS messages
   │   │   ├── AT+CMGD=1,4        - Delete all SMS messages
   │   │   └── AT+CMGD=<index>    - Delete SMS by index
   │   └── SMS Content
   │       ├── AT+CMGS="<number>" - Send SMS to number
   │       ├── >Message Text      - Type message content
   │       └── Ctrl+Z             - Send message (ASCII 26 or 0x1A)
   │
   ├── GPRS & Internet
   │   ├── TCP/IP Mode Setup
   │   │   └── AT+QIMODE=0        - Set TCP/IP mode to non-transparent 
   │   ├── APN Configuration
   │   │   ├── AT+QIREGAPP        - Start TCP/IP registration
   │   │   ├── AT+QICSGP=1,"APN"  - Set GPRS APN
   │   │   └── AT+QICSGP?         - Show current GPRS context settings
   │   ├── Connection Management
   │   │   ├── AT+QIACT            - Activate GPRS context
   │   │   ├── AT+QIDEACT          - Deactivate GPRS context
   │   │   └── AT+QILOCIP          - Get local IP address
   │   └── Network Status
   │       ├── AT+QISTATE          - Query connection status
   │       └── AT+QIDEACT=1        - Deactivate specific context
   │   
   ├── MQTT Operations
   │   ├── MQTT Configuration
   │   │   └── AT+QMTCFG="keepalive",0,120 - Configure MQTT keep-alive timer
   │   ├── MQTT Connection
   │   │   ├── AT+QMTOPEN=0,"<IP>","<PORT>" - Opens MQTT connection to the server
   │   │   └── AT+QMTCONN=0,"<ClientID>","<Username>","<Password>" - Connects to MQTT broker
   │   ├── MQTT Messaging
   │   │   └── AT+QMTPUB=0,0,0,0,"<Topic>" - Publishes data to a specific MQTT topic
   │   ├── MQTT Status Monitoring
   │   │   ├── AT+QMTOPEN?          - Check MQTT open status
   │   │   ├── AT+QMTCONN?          - Check MQTT connection status  
   │   │   └── AT+QMTPUB?           - Check MQTT publish status
   │   └── MQTT Disconnect
   │       └── AT+QMTDISC=0       - Disconnect MQTT session
   │
   └── System Information
       ├── AT+GSV                 - Get module version
       ├── AT+GMI                 - Get manufacturer info
       ├── AT+GMM                 - Get model identification
       ├── AT+GSN                 - Get IMEI number
       ├── AT+CIMI                - Get SIM IMSI
       ├── AT+CCID                - Get SIM card ID
       ├── AT+CBC                 - Get battery charge
       └── AT+CCLK?               - Get current time
```

> [!IMPORTANT]
> When sending AT commands to the module, **it is essential to append the carriage return (`\r`) and newline (`\n`) characters at the end of each command**.
> These termination characters ensure proper interpretation by the module and prevent command processing errors.
>
> Failing to include `\r\n` may result in the module not recognizing or executing the command correctly.
> 
> Example:
> ```
> AT\r\n
> ```
> Make sure to follow this format to ensure seamless communication with the module.

> [!CAUTION]
> When the module responds to an AT command, **it always includes at least one carriage return (`\r`) and newline (`\n`) at the beginning and end of the response**. These characters ensure proper formatting and readability of the response.
> 
> ### Important Notes:
> - The **minimum** termination format is `\r\n` at the start and end of the response.
> - Depending on the specific command, the module **may include additional `\r\n` sequences** within the response.
> - Ensure your parsing logic accounts for these extra characters to avoid unexpected behavior.
> 
> #### Example Response:
> ```
> \r\nOK\r\n
> ```
> 
> For commands with more complex outputs, multiple `\r\n` sequences might be present.
> 
> Keeping this in mind will help maintain smooth communication between your system and the module.


# 📡 **Basic AT Commands**
These are used to test the communication between your microcontroller and the GSM/GPRS module, disable echo for cleaner output, and enable detailed error reporting for debugging.

| Command         | Description                             |
| --------------- | --------------------------------------- |
| `AT`            | Test command to check communication.    |
| `ATE0`          | Turn off command echo.                  |
| `AT+CMEE=2`     | Enable verbose error messages.          |
| `AT+IPR=115200` | Set fixed UART baud rate to 115200 bps. |


## ✅ `AT`

| **Description**       | Test if the module is connected and responsive. |
| --------------------- | ----------------------------------------------- |
| **Syntax**            | `AT`                                            |
| **Parameters**        | None                                            |
| **Expected Response** | `OK` if the module is working properly.         |
| **Error Response**    | No response or `ERROR` if communication fails.  |

**Explanation:**
This is the most fundamental AT command. It is used to verify if the GSM module is powered on, initialized correctly, and can communicate with the microcontroller or terminal. If everything is okay, the module replies with `OK`.
If you get no response or garbage values, check:

* Baud rate mismatch
* Wrong UART pins
* Power supply instability

## ✅ `ATE0`

| **Description**       | Disable command echo.           |
| --------------------- | ------------------------------- |
| **Syntax**            | `ATE0`                          |
| **Parameters**        | `0` = Disable echo              |
| **Expected Response** | `OK`                            |
| **Error Response**    | `ERROR` if the syntax is wrong. |

**Explanation:**
By default, the module echoes back any command you send. For example, if you send `AT`, it may respond with:

```
AT
OK
```

This is not ideal for parsing responses in software. Sending `ATE0` disables the echo, so you only get:

```
OK
```

This simplifies serial communication between the module and a microcontroller or script.

## ✅ `AT+CMEE=2`

| **Description** | Enable verbose error messages. |
| --------------- | ------------------------------ |
| **Syntax**      | `AT+CMEE=<n>`                  |
| **Parameters**  | `0` = Disable (default)        |

```
                `1` = Numeric error codes  
                `2` = Verbose (human-readable) error strings |
```

\| **Expected Response** | `OK`                       |
\| **Error Response** | `ERROR` if unsupported or wrongly formatted. |

**Explanation:**
This command configures how the module displays error messages.
Setting `AT+CMEE=2` allows you to get meaningful error messages like:

```
+CME ERROR: SIM not inserted
```

Instead of just:

```
ERROR
```

This is extremely useful for debugging and understanding issues related to SIM card, network registration, or GPRS.


## ✅ `AT+IPR=115200`

| **Description**       | Set the UART baud rate to 115200 bps.        |
| --------------------- | -------------------------------------------- |
| **Syntax**            | `AT+IPR=<rate>`                              |
| **Parameters**        | `<rate>` = Baud rate, e.g., `9600`, `115200` |
| **Expected Response** | `OK`                                         |
| **Error Response**    | `ERROR` if the value is not supported.       |

**Explanation:**
This sets the communication speed between your microcontroller and the GSM module. The commonly used rate is `115200`, which ensures fast and reliable data transfer:

```
AT+IPR=115200
```

Make sure your microcontroller UART is also configured to `115200 bps` after setting this.

> [!Tip]
> If supported, save the setting using `AT&W` so it persists after reboot.

## 📝 Summary Table

| Command         | Purpose                          | Expected Response | Usage Hint                                |
| --------------- | -------------------------------- | ----------------- | ----------------------------------------- |
| `AT`            | Check basic communication        | `OK`              | First command to test module connectivity |
| `ATE0`          | Disable command echo             | `OK`              | Send before parsing AT replies            |
| `AT+CMEE=2`     | Enable verbose error reporting   | `OK`              | Helps identify SIM/network issues         |
| `AT+IPR=115200` | Set UART baud rate to 115200 bps | `OK`              | Match baud rate on MCU/terminal side      |

# 📲 **SIM and Network Initialization**
This set handles SIM card readiness, enables full module functionality, checks signal strength, verifies network registration, and identifies the current network operator—essential for ensuring cellular connectivity before using data services.

| Command         | Description                        |
| --------------- | ---------------------------------- |
| `AT+CPIN?`      | Check SIM card status.             |
| `AT+CPIN="PIN"` | Enter SIM PIN.                     |
| `AT+CFUN=1`     | Set full functionality mode.       |
| `AT+CSQ`        | Check signal quality.              |
| `AT+CREG?`      | Check network registration status. |
| `AT+COPS?`      | Get current operator.              |


## ✅ `AT+CPIN?`

| **Description**                         | Check SIM card status.                  |
| --------------------------------------- | --------------------------------------- |
| **Syntax**                              | `AT+CPIN?`                              |
| **Parameters**                          | None                                    |
| **Expected Response**                   |                                         |
| `+CPIN: READY` → SIM is ready           |                                         |
| `+CPIN: SIM PIN` → SIM requires PIN     |                                         |
| `+CPIN: SIM PUK` → SIM is locked        |                                         |
| `+CPIN: NOT INSERTED` → No SIM detected |                                         |
| Followed by `OK`                        |                                         |
| **Error Response**                      | `ERROR` if the command is not accepted. |

**Explanation:**
This command tells you the current status of the SIM card. It’s one of the first checks after powering up the module. If `+CPIN: READY`, the SIM is present and usable.

## ✅ `AT+CPIN="PIN"`

| **Description**       | Enter SIM PIN code if required.        |
| --------------------- | -------------------------------------- |
| **Syntax**            | `AT+CPIN="<PIN>"`                      |
| **Parameters**        | `<PIN>` – The ۴-digit SIM PIN code     |
| **Expected Response** | `OK` if PIN accepted                   |
| **Error Response**    | `ERROR` if incorrect PIN or locked SIM |

**Explanation:**
This command is used when the SIM is locked and requires a PIN to proceed. If `AT+CPIN?` returns `SIM PIN`, use this command to unlock the SIM card.

## ✅ `AT+CFUN=1`

| **Description**                                         | Set full functionality mode (enable RF). |
| ------------------------------------------------------- | ---------------------------------------- |
| **Syntax**                                              | `AT+CFUN=<mode>`                         |
| **Parameters**                                          |                                          |
| `0` = Minimum functionality (turn off RF)               |                                          |
| `1` = Full functionality (default)                      |                                          |
| `4` = Disable phone functionality (e.g., airplane mode) |                                          |
| **Expected Response**                                   | `OK`                                     |
| **Error Response**                                      | `ERROR` if incorrect or unsupported.     |

**Explanation:**
This command enables or disables different levels of module functionality.
To make calls, use SMS, or connect to GPRS, the module must be in full mode (`AT+CFUN=1`).

## ✅ `AT+CSQ`

| **Description**       | Check signal quality (RSSI and BER). |
| --------------------- | ------------------------------------ |
| **Syntax**            | `AT+CSQ`                             |
| **Parameters**        | None                                 |
| **Expected Response** | `+CSQ: <rssi>,<ber>`                 |
| `OK`                  |                                      |
| Where:                |                                      |

* `<rssi>` = Received signal strength (0–31, 99=unknown)
* `<ber>` = Bit error rate (0–7, 99=unknown) |
  \| **Error Response**  | `ERROR` if unsupported.                         |

**Explanation:**
This is useful to monitor how good the cellular signal is. For RSSI:

* `10–14` is acceptable
* `15–19` is good
* `20–30` is excellent
  A poor signal might prevent network registration or stable GPRS connection.

## ✅ `AT+CREG?`

| **Description**       | Check network registration status (home or roaming). |
| --------------------- | ---------------------------------------------------- |
| **Syntax**            | `AT+CREG?`                                           |
| **Parameters**        | None                                                 |
| **Expected Response** |                                                      |
| `+CREG: <n>,<stat>`   |                                                      |
| `OK`                  |                                                      |
| Where:                |                                                      |

* `<stat>` =
  `0` = Not registered
  `1` = Registered (home)
  `2` = Searching
  `3` = Registration denied
  `4` = Unknown
  `5` = Registered (roaming) |
  \| **Error Response**  | `ERROR` if unsupported.                               |

**Explanation:**
Use this to check if the module is successfully registered on the GSM network. You need `1` or `5` to start any communication (call/SMS/data).

## ✅ `AT+COPS?`

| **Description**                            | Get current mobile operator. |
| ------------------------------------------ | ---------------------------- |
| **Syntax**                                 | `AT+COPS?`                   |
| **Parameters**                             | None                         |
| **Expected Response**                      |                              |
| `+COPS: <mode>,<format>,"<operator name>"` |                              |
| `OK`                                       |                              |
| Where:                                     |                              |

* `<mode>` = Operator selection mode (e.g., 0=auto)
* `<format>` = Format of operator name (e.g., 0=long alphanumeric)
* `<operator name>` = Name of currently connected operator |
  \| **Error Response**  | `ERROR` if network not selected or command fails. |

**Explanation:**
Helps identify which operator the module is currently connected to. Very useful in roaming environments or when testing SIM cards with different operators.

## 📋 Summary Table

| Command          | Function                    | Sample Reply          | Purpose                                |
| ---------------- | --------------------------- | --------------------- | -------------------------------------- |
| `AT+CPIN?`       | Check SIM status            | `+CPIN: READY`        | Ensure SIM is active and detected      |
| `AT+CPIN="1234"` | Enter SIM PIN code          | `OK`                  | Unlock SIM card with PIN               |
| `AT+CFUN=1`      | Set full functionality      | `OK`                  | Enable RF and full features            |
| `AT+CSQ`         | Signal quality              | `+CSQ: 18,0`          | Check signal strength and link quality |
| `AT+CREG?`       | Network registration status | `+CREG: 0,1`          | Verify connection to GSM network       |
| `AT+COPS?`       | Current operator            | `+COPS: 0,0,"IR-MCI"` | Display active cellular provider       |


# ✉️ **SMS Configuration and Control**
These commands configure the module for sending and receiving SMS in text mode, define the character set, manage SMS storage, and set formatting parameters depending on the mobile operator.

| Command              | Description                                   |
| -------------------- | --------------------------------------------- |
| `AT+CMGF=1`          | Set SMS mode to text.                         |
| `AT+CSCS="GSM"`      | Set character set to GSM.                     |
| `AT+CMGD=1,4`        | Delete all SMS messages.                      |
| `AT+CSMP=17,167,0,0` | SMS text mode parameters (MCI, MTN, default). |
| `AT+CSMP=17,167,0,4` | SMS text mode parameters (Rightel).           |
| `AT+CMTI`            | Incoming SMS indication.                      |
| `AT+CMGR=<index>`    | Reads an SMS message from memory.             |
| `AT+CMGS="<number>"` | Sends an SMS to the specified number.         |

## ✅ `AT+CMGF=1`

| **Description**                             | Set SMS message format to **text mode**. |
| ------------------------------------------- | ---------------------------------------- |
| **Syntax**                                  | `AT+CMGF=<mode>`                         |
| **Parameters**                              |                                          |
| `0` = PDU mode (Protocol Data Unit, binary) |                                          |
| `1` = Text mode (human-readable)            |                                          |
| **Expected Response**                       | `OK`                                     |
| **Error Response**                          | `ERROR` if the mode is not supported.    |

**Explanation:**
This command sets the SMS mode. For most applications and easier debugging or testing, **text mode** is preferred.
In text mode, messages can be written and read in plain ASCII/GSM characters.

## ✅ `AT+CSCS="GSM"`

| **Description**                                 | Select the **character set** used for text mode SMS. |
| ----------------------------------------------- | ---------------------------------------------------- |
| **Syntax**                                      | `AT+CSCS="<charset>"`                                |
| **Parameters**                                  | `"GSM"` = Default 7-bit GSM alphabet (basic set)     |
| `"IRA"` = International Reference Alphabet      |                                                      |
| `"UCS2"` = Unicode (UTF-16, for extended chars) |                                                      |
| **Expected Response**                           | `OK`                                                 |
| **Error Response**                              | `ERROR` if the charset is not supported.             |

**Explanation:**
This ensures the character encoding matches what the module and network expect.
For simple English text messages, `"GSM"` is most efficient.
Use `"UCS2"` if you plan to send Persian, Arabic, or other non-Latin characters.

## ✅ `AT+CMGD=1,4`

| **Description**                                        | Delete **all SMS messages** stored in memory. |
| ------------------------------------------------------ | --------------------------------------------- |
| **Syntax**                                             | `AT+CMGD=<index>,<delflag>`                   |
| **Parameters**                                         |                                               |
| `<index>` = Start index to delete from (typically `1`) |                                               |
| `<delflag>` =                                          |                                               |

* `0` = Delete only message at index
* `1` = Delete all read messages
* `2` = Delete all read + sent
* `3` = Delete all read + sent + unsent
* `4` = Delete **all messages** |
  \| **Expected Response** | `OK`                                              |
  \| **Error Response**  | `ERROR` if memory access fails.                      |

**Explanation:**
This command clears the message inbox on the SIM or module memory.
Very useful before testing, or to prevent full memory blocking new messages.

## ✅ `AT+CSMP=17,167,0,0` (For MCI, MTN, etc.)

| **Description** | Set **SMS text parameters** (basic/default). |
| --------------- | -------------------------------------------- |
| **Syntax**      | `AT+CSMP=<fo>,<vp>,<pid>,<dcs>`              |
| **Parameters**  |                                              |

* `fo = 17` → Message header settings
* `vp = 167` → Validity period (maximum)
* `pid = 0` → Protocol ID (0 = default)
* `dcs = 0` → Data Coding Scheme (0 = GSM 7-bit) |
  \| **Expected Response** | `OK`                                             |
  \| **Error Response**  | `ERROR` if values are out of range or unsupported.  |

**Explanation:**
This sets default SMS sending behavior. For most Iranian operators like **MCI** and **MTN**, this is the typical configuration for English messages.

## ✅ `AT+CSMP=17,167,0,4` (For Rightel)

| **Description**       | Set **SMS text parameters** for Rightel.            |
| --------------------- | --------------------------------------------------- |
| **Syntax**            | `AT+CSMP=17,167,0,4`                                |
| **Parameters**        | Same as above, except `dcs = 4` → 8-bit data format |
| **Expected Response** | `OK`                                                |
| **Error Response**    | `ERROR` if encoding is not supported.               |

**Explanation:**
Rightel may require 8-bit encoding (`dcs=4`) for proper handling of certain SMS messages.
This can avoid garbled or broken text in some modules/networks.

## ✅ `AT+CMTI`

| **Description**       | **Indicates new incoming SMS message**.   |
| --------------------- | ----------------------------------------- |
| **Syntax**            | `AT+CMTI="<mem>",<index>`                 |
| **Parameters**        |                                           |
| `<mem>` = `"SM"`      | SIM card memory                           |
| `<index>` = Number    | Index of the received message             |
| **Expected Response** | `+CMTI: "SM",3` (example)                 |
| **Error Response**    | `ERROR` if unsolicited result code fails. |

**Explanation:**
This is an **unsolicited** notification that appears when a new SMS arrives.
Use the given `<index>` with `AT+CMGR` to read the message.
Some modules require `AT+CNMI=2,1,0,0,0` beforehand to enable this.

## ✅ `AT+CMGR=<index>`

| **Description**           | **Reads** an SMS message from memory.     |
| ------------------------- | ----------------------------------------- |
| **Syntax**                | `AT+CMGR=<index>`                         |
| **Parameters**            |                                           |
| `<index>` = Message index | (e.g., from `AT+CMTI` response)           |
| **Expected Response**     | Header and text of the message            |
| **Error Response**        | `ERROR` if the index is invalid or empty. |

**Example Response:**

```
+CMGR: "REC UNREAD","+989123456789","","24/05/15,14:00:00+03"
Hello from Modem!
```

**Explanation:**
Reads the stored SMS at a given index. If status is `"REC UNREAD"`, it becomes `"REC READ"` after this command.

## ✅ `AT+CMGS="<number>"`

| **Description**       | **Sends** an SMS message to a phone number.    |
| --------------------- | ---------------------------------------------- |
| **Syntax**            | `AT+CMGS="<recipient_number>"`                 |
| **Expected Prompt**   | `>` (waiting for message text)                 |
| **Message End**       | Send **CTRL+Z** (`0x1A`) to finish the message |
| **Expected Response** | `+CMGS: <mr>` followed by `OK`                 |
| **Error Response**    | `ERROR` if sending fails                       |

**Example:**

```bash
AT+CMGS="+989123456789"
>Hello from USART!<CTRL+Z>
```

**Explanation:**
After issuing this command, the modem waits for the message body.
End the message with **CTRL+Z**. You must first run `AT+CMGF=1` and other init commands before this.


## 🧾 Summary Table

| Command              | Purpose                   | Notes                                           |
| -------------------- | ------------------------- | ----------------------------------------------- |
| `AT+CMGF=1`          | Use **text mode** for SMS | Easier to use and debug than PDU mode           |
| `AT+CSCS="GSM"`      | Set **character set**     | Use `"GSM"` for English, `"UCS2"` for Persian   |
| `AT+CMGD=1,4`        | Delete all messages       | Clears memory before tests                      |
| `AT+CSMP=17,167,0,0` | SMS config for MCI, MTN   | Use for standard 7-bit text messages            |
| `AT+CSMP=17,167,0,4` | SMS config for Rightel    | Needed if text appears broken or unsupported    |
| `AT+CMTI`            | Incoming SMS notification | Triggers when a message is received             |
| `AT+CMGR=<index>`    | Read SMS message          | Use after `AT+CMTI` or to manually check memory |
| `AT+CMGS="<number>"` | Send SMS message          | Use after text-mode and parameter configuration |


# 📞 **Call-Related AT Commands**

These commands are used to make and receive voice calls, detect incoming calls, answer or hang up calls, and display caller ID information. They are essential for enabling GSM voice call functionality in microcontroller projects.

## 📋 Command Overview (Updated)

| Command         | Description                             |
| --------------- | --------------------------------------- |
| `ATD<number>;`  | Dial a number.                          |
| `ATA`           | Answer an incoming call.                |
| `ATH`           | Hang up an ongoing call.                |
| `AT+CLCC`       | Query current call status.              |


## ✅ `ATD<number>;`

| **Description**       | Dial a number for a voice call.         |
| --------------------- | --------------------------------------- |
| **Syntax**            | `ATD<number>;`                          |
| **Parameters**        | `<number>` = target phone number        |
| **Expected Response** | `OK` if the command is accepted         |
| **Call Status**       | `RINGING`, then `CONNECTED` if answered |
| **Error Response**    | `NO CARRIER`, `BUSY`, or `NO DIALTONE`  |

**Example:**

```txt
ATD+98912345678;
```

**Explanation:**
This command initiates a voice call to the specified number. The semicolon `;` is necessary to indicate a **voice** call instead of a data call.

## ✅ `ATA`

| **Description**       | Answer an incoming voice call. |
| --------------------- | ------------------------------ |
| **Syntax**            | `ATA`                          |
| **Parameters**        | None                           |
| **Expected Response** | `OK`, followed by `CONNECTED`  |
| **Error Response**    | `ERROR` if no call is waiting  |

**Explanation:**
When the module receives a call and sends `RING`, issuing `ATA` will answer the call.


## ✅ `ATH`

| **Description**       | Hang up the current or incoming call. |
| --------------------- | ------------------------------------- |
| **Syntax**            | `ATH`                                 |
| **Parameters**        | None                                  |
| **Expected Response** | `OK`                                  |
| **Error Response**    | `ERROR` if no call is in progress     |

**Explanation:**
This command ends any ongoing voice call or cancels an incoming call before answering.


## ✅ `AT+CLIP=1`

| **Description**       | Enable caller ID for incoming calls.          |
| --------------------- | --------------------------------------------- |
| **Syntax**            | `AT+CLIP=1`                                   |
| **Parameters**        | `1` = Enable caller ID                        |
| **Expected Response** | `OK`, and `+CLIP: "+number"` on incoming call |
| **Error Response**    | `ERROR` if unsupported                        |

**Explanation:**
Once this command is enabled, when a call comes in, the module will output:

```txt
RING
+CLIP: "+1234567890",145,"",,"",0
```

This allows your system to log or react based on the caller's phone number.


## 📝 Summary Table

| Command         | Purpose                            | Expected Response  | Usage Hint                                   |
| --------------- | ---------------------------------- | ------------------ | -------------------------------------------- |
| `ATD<number>;`  | Dial a voice call                  | `OK`               | Semicolon `;` indicates voice call           |
| `ATA`           | Answer an incoming call            | `OK`               | When `RING` is received                      |
| `ATH`           | Hang up an active or incoming call | `OK`               | Ends or rejects call                         |
| `AT+CLIP=1`     | Show caller ID on incoming calls   | `OK`, then `+CLIP` | Enables call source detection                |


# 🌐 **TCP/IP and GPRS Configuration**
These commands prepare the module for internet access over GPRS. They configure the IP mode, activate the network context, and obtain the module’s local IP address necessary for TCP/UDP communication.

| Command             | Description                         |
| ------------------- | ----------------------------------- |
| `AT+QIMODE=0`       | Set TCP/IP mode to non-transparent. |
| `AT+QIREGAPP`       | Start TCP/IP registration.          |
| `AT+QICSGP=1,"APN"` | Set GPRS APN.                       |
| `AT+QICSGP?`        | Show current GPRS context settings. |
| `AT+QIACT`          | Activate GPRS context.              |
| `AT+QILOCIP`        | Get local IP address.               |

## ✅ `AT+QIMODE=0`

| **Description**                                          | Set **TCP/IP mode** to **non-transparent** mode. |
| -------------------------------------------------------- | ------------------------------------------------ |
| **Syntax**                                               | `AT+QIMODE=<mode>`                               |
| **Parameters**                                           |                                                  |
| `0` = Non-transparent mode (data is handled by commands) |                                                  |
| `1` = Transparent mode (raw data stream)                 |                                                  |
| **Expected Response**                                    | `OK`                                             |
| **Error Response**                                       | `ERROR` if an invalid mode is used.              |

**Explanation:**
In non-transparent mode (`0`), you send and receive data using AT commands like `AT+QISEND`.
This mode is more controlled and preferred in **microcontroller-based** applications.

## ✅ `AT+QIREGAPP`

| **Description** | **Register** with the GPRS network using APN.   |
| --------------- | ----------------------------------------------- |
| **Syntax**      | `AT+QIREGAPP="<APN>","<username>","<password>"` |
| **Parameters**  |                                                 |

* `<APN>` = Access Point Name (e.g. `mcinet`, `mtnirancell`, `rightel`)
* `<username>` = GPRS login name (often empty `" "`)
* `<password>` = GPRS login password (often empty `" "`) |
  \| **Expected Response** | `OK`                                              |
  \| **Error Response**  | `ERROR` if SIM is not ready, or APN is wrong.        |

**Explanation:**
This command **sets and registers** your GPRS credentials.
Without this, you cannot activate GPRS (which is required before using sockets).

📝 Example:

```bash
AT+QIREGAPP="mcinet","",""
```

## ✅ `AT+QICSGP=1,"APN"`

| **Description**       | Set the **GPRS context** profile including APN, username, and password. |
| --------------------- | ----------------------------------------------------------------------- |
| **Syntax**            | `AT+QICSGP=1,"<APN>","<username>","<password>"`                         |
| **Parameters**        |                                                                         |
| `1`                   | PDP context ID (usually `1` for the default context)                    |
| `<APN>`               | Access Point Name (e.g., `"mcinet"`, `"mtnirancell"`, `"rightel"`)      |
| `<username>`          | GPRS username (usually empty string `""`)                               |
| `<password>`          | GPRS password (usually empty string `""`)                               |
| **Expected Response** | `OK`                                                                    |
| **Error Response**    | `ERROR` if the parameters are invalid or SIM is not ready               |

**Explanation:**
This command configures the **GPRS context profile** required to establish a data connection. It is often used **as an alternative to** `AT+QIREGAPP`, especially in newer modules where `QIREGAPP` is deprecated or not supported.
Once this is set, the profile can be **activated using `AT+QIACT`**, enabling internet connectivity.

📝 Example:

```bash
AT+QICSGP=1,"mcinet","",""
```

📌 **Note:**
Always configure this **before** attempting to activate the data connection (`AT+QIACT`). You can verify the configuration using `AT+QICSGP?`.

## ✅ `AT+QICSGP?`

| **Description**       | Query the **current GPRS settings** (APN, username). |
| --------------------- | ---------------------------------------------------- |
| **Syntax**            | `AT+QICSGP?`                                         |
| **Parameters**        | None                                                 |
| **Expected Response** |                                                      |
| Example:              |                                                      |

```
+QICSGP: "mcinet","",""
OK
```

\| **Error Response**  | `ERROR` if GPRS profile is not set.                   |

**Explanation:**
Used to **verify the current GPRS configuration**.
You can use this command to check whether your APN settings were accepted.

## ✅ `AT+QIACT`

| **Description**       | **Activate** the GPRS context (start data session). |
| --------------------- | --------------------------------------------------- |
| **Syntax**            | `AT+QIACT`                                          |
| **Parameters**        | None                                                |
| **Expected Response** | `OK`                                                |
| **Error Response**    | `ERROR` if the SIM is not registered or APN failed. |

**Explanation:**
This command actually **opens the data connection** to the GPRS network.
Think of it as enabling your mobile "data" after inserting SIM and registering APN.

🔍 Important:
Make sure the SIM has enough signal and has successfully attached to the network (check using `AT+CREG?` before this step).

## ✅ `AT+QILOCIP`

| **Description**       | Query the **local IP address** assigned to the module. |
| --------------------- | ------------------------------------------------------ |
| **Syntax**            | `AT+QILOCIP`                                           |
| **Parameters**        | None                                                   |
| **Expected Response** |                                                        |
| Example:              |                                                        |

```
10.145.88.42  
OK
```

\| **Error Response**  | `ERROR` if GPRS is not active or IP not assigned.      |

**Explanation:**
After GPRS activation, the operator assigns a **local IP address**.
This command lets you confirm that IP address, which is essential before opening a socket.

## 🧾 Summary Table

| Command             | Purpose                          | Notes                                                    |
| ------------------- | -------------------------------- | -------------------------------------------------------- |
| `AT+QIMODE=0`       | Set non-transparent TCP/IP mode  | Recommended for microcontroller-controlled communication |
| `AT+QIREGAPP`       | Register APN with GPRS           | Older method; may not work on newer modules              |
| `AT+QICSGP=1,"APN"` | Set GPRS APN profile             | Preferred in modern modules; replaces `QIREGAPP`         |
| `AT+QICSGP?`        | Show current APN, username, pass | Helps verify config before connection                    |
| `AT+QIACT`          | Activate GPRS session            | Must be successful to get IP or use sockets              |
| `AT+QILOCIP`        | Get IP address assigned via GPRS | Confirms that the connection to the network is active    |

# ☁️ **MQTT Configuration and Status**
This category includes commands to set MQTT session parameters (like keepalive), check the status of socket and MQTT connections, monitor publish status, and properly disconnect—essential for IoT data exchange via MQTT protocol.

| Command                                               | Description                              |
| ----------------------------------------------------- | ---------------------------------------- |
| `AT+QMTCFG="keepalive",0,120`                         | Configure MQTT keep-alive timer.         |
| `AT+QMTOPEN?`                                         | Check MQTT open status.                  |
| `AT+QMTCONN?`                                         | Check MQTT connection status.            |
| `AT+QMTPUB?`                                          | Check MQTT publish status.               |
| `AT+QMTDISC=0`                                        | Disconnect MQTT session.                 |
| `AT+QMTOPEN=0,"<IP>","<PORT>"`                        | Opens MQTT connection to the server.     |
| `AT+QMTCONN=0,"<ClientID>","<Username>","<Password>"` | Connects to MQTT broker.                 |
| `AT+QMTPUB=0,0,0,0,"<Topic>"`                         | Publishes data to a specific MQTT topic. |         


## ✅ `AT+QMTCFG="keepalive",0,120`

| **Description** | Configure the MQTT **keep-alive timer** (heartbeat). |
| --------------- | ---------------------------------------------------- |
| **Syntax**      | `AT+QMTCFG="keepalive",<client_idx>,<time>`          |
| **Parameters**  |                                                      |

* `"keepalive"` = keyword to configure keep-alive
* `<client_idx>` = MQTT client index (usually `0`)
* `<time>` = Keep-alive interval in seconds (e.g., `120`) |
  \| **Expected Response** | `OK`                                               |
  \| **Error Response**  | `ERROR` if parameters are invalid.                   |

**Explanation:**
This sets how often the MQTT client will send a **ping** to the broker to keep the connection alive.
For example, `AT+QMTCFG="keepalive",0,120` means:

> Client 0 sends a keepalive ping every 120 seconds.

## ✅ `AT+QMTOPEN?`

| **Description**       | Check the status of the **MQTT socket connection**. |
| --------------------- | --------------------------------------------------- |
| **Syntax**            | `AT+QMTOPEN?`                                       |
| **Parameters**        | None                                                |
| **Expected Response** |                                                     |
| Example:              |                                                     |

```
+QMTOPEN: 0,0  
OK
```

\| **Meaning**         |

* `0` (first) = Client index
* `0` (second) = Open success

> Values:
> `0` = success
> `1` = still connecting
> `-1` = failed |
> \| **Error Response**  | `ERROR` if no MQTT session is initiated.              |

**Explanation:**
This is used to confirm whether the module has successfully **opened a TCP connection** to the MQTT broker before authentication.

## ✅ `AT+QMTCONN?`

| **Description**       | Check **MQTT connection status** after opening socket. |
| --------------------- | ------------------------------------------------------ |
| **Syntax**            | `AT+QMTCONN?`                                          |
| **Expected Response** |                                                        |
| Example:              |                                                        |

```
+QMTCONN: 0,0  
OK
```

\| **Meaning**         |

* `0` (first) = Client index
* `0` (second) = MQTT connection established

> Values:
> `0` = connected
> `1` = disconnected
> `2` = connection refused |
> \| **Error Response**  | `ERROR` if MQTT not opened first.                      |

**Explanation:**
Use this to **verify that MQTT authentication** (username, password, client ID) has been accepted by the broker.

## ✅ `AT+QMTPUB?`

| **Description**       | Check **MQTT publish status**. |
| --------------------- | ------------------------------ |
| **Syntax**            | `AT+QMTPUB?`                   |
| **Expected Response** |                                |
| Example:              |                                |

```
+QMTPUB: 0,0,0  
OK
```

\| **Meaning**         |

* First `0` = Client index
* Second `0` = Message ID
* Third `0` = Result (0 = success) |
  \| **Error Response**  | `ERROR` if no publish has occurred.                    |

**Explanation:**
After sending an MQTT publish command, this query returns the **result of the last publish**, useful for debugging reliability.

## ✅ `AT+QMTDISC=0`

| **Description** | **Disconnect** the MQTT client from the broker. |
| --------------- | ----------------------------------------------- |
| **Syntax**      | `AT+QMTDISC=<client_idx>`                       |
| **Parameters**  |                                                 |

* `<client_idx>` = MQTT client index (e.g., `0`) |
  \| **Expected Response** |

```
OK  
+QMTDISC: 0,0
```

\| **Meaning**         | `0` = disconnected successfully |
\| **Error Response**  | `ERROR` if already disconnected or client not open.    |

**Explanation:**
Always cleanly disconnect using this command before restarting or shutting down the module to avoid session timeout or lingering sessions on the broker.

## ✅ `AT+QMTOPEN=0,"<IP>","<PORT>"`

| **Description** | Open the **MQTT socket connection** to the broker/server. |
| --------------- | --------------------------------------------------------- |
| **Syntax**      | `AT+QMTOPEN=<client_idx>,"<IP>","<PORT>"`                 |
| **Parameters**  |                                                           |

* `<client_idx>` = MQTT client index (usually `0`)
* `<IP>` = IP address or domain of the MQTT broker (e.g., `"mqtt.example.com"`)
* `<PORT>` = Port number (e.g., `1883` for unsecured, `8883` for TLS)

\| **Expected Response** |

```
OK
+QMTOPEN: 0,0
```

* `0` = client index
* `0` = socket opened successfully

\| **Error Response**    | `+QMTOPEN: 0,-1` (failure) or `ERROR` for invalid syntax |

**Explanation:**
This command initializes the **TCP connection** to the MQTT broker. It must be called **before authentication** with `AT+QMTCONN`.

---

## ✅ `AT+QMTCONN=0,"<ClientID>","<Username>","<Password>"`

| **Description** | Establish full **MQTT session authentication** with the broker.  |
| --------------- | ---------------------------------------------------------------- |
| **Syntax**      | `AT+QMTCONN=<client_idx>,"<ClientID>","<Username>","<Password>"` |
| **Parameters**  |                                                                  |

* `<client_idx>` = MQTT client index (e.g., `0`)
* `<ClientID>` = Client ID string (must be unique per device)
* `<Username>` = Username used for MQTT authentication
* `<Password>` = Password used for MQTT authentication

\| **Expected Response** |

```
OK
+QMTCONN: 0,0,0
```

* First `0` = client index
* Second `0` = connection result
* Third `0` = session present flag

> Connection result values:
> `0` = success, `1` = refused/unavailable, `2` = bad credentials

\| **Error Response**    | `+QMTCONN: 0,-1` or `ERROR` if connection setup fails |

**Explanation:**
Use this to complete **MQTT login** after opening the socket. This step includes sending the client ID and credentials. Ensure APN and network are active first.

---

## ✅ `AT+QMTPUB=0,0,0,0,"<Topic>"`

| **Description** | Publish a message to a specific **MQTT topic**.            |
| --------------- | ---------------------------------------------------------- |
| **Syntax**      | `AT+QMTPUB=<client_idx>,<msg_id>,<qos>,<retain>,"<topic>"` |
| **Parameters**  |                                                            |

* `<client_idx>` = MQTT client index (e.g., `0`)
* `<msg_id>` = Message ID (use `0` for auto-ID)
* `<qos>` = Quality of Service (0, 1, or 2)
* `<retain>` = Retain flag (0 = no retain, 1 = retain message)
* `<topic>` = MQTT topic string (e.g., `"sensor/temp"`)

\| **Expected Response** |

```
>  // Waiting for data input
<Your MQTT message here>
Ctrl+Z (ASCII 26)
+QMTPUB: 0,0,0
OK
```

* First `0` = client index
* Second `0` = message ID
* Third `0` = publish success (0 = OK)

\| **Error Response**    | `ERROR` if socket is not ready, topic is invalid, or publish failed |

**Explanation:**
This sends data to a broker under the specified topic. After executing this command, the modem waits for the **message payload**, which must be followed by **Ctrl+Z** to complete the publish.


## 📊 Summary Table

| Command                                  | Purpose                          | Example Use                             |
| ---------------------------------------- | -------------------------------- | --------------------------------------- |
| `AT+QMTCFG="keepalive",0,120`            | Set MQTT keep-alive timer        | Keep session alive with ping every ١٢٠s |
| `AT+QMTOPEN=0,"mqtt.example.com","1883"` | Open socket to MQTT broker       | Connects TCP layer to broker            |
| `AT+QMTOPEN?`                            | Check socket open status         | `+QMTOPEN: 0,0` = open success          |
| `AT+QMTCONN=0,"Client123","user","pass"` | Authenticate MQTT connection     | Connects using credentials              |
| `AT+QMTCONN?`                            | Check MQTT authentication status | `+QMTCONN: 0,0` = connected             |
| `AT+QMTPUB=0,0,0,0,"sensor/temp"`        | Publish to MQTT topic            | Sends data after prompt                 |
| `AT+QMTPUB?`                             | Verify last publish result       | `+QMTPUB: 0,0,0` = success              |
| `AT+QMTDISC=0`                           | Disconnect MQTT session          | Clean shutdown; releases session        |


# ✅ **🔌 Step-by-Step AT Command Sequence**

This section provides a complete, structured AT command sequence to initialize a GSM/GPRS module and connect it to an MQTT broker. Each step includes commands, explanations, expected responses, and helpful usage tips.


## **1. Power-up and Basic Check**
Ensure the module is communicating properly with your microcontroller or terminal.

```plaintext
AT                      // Test communication
ATE0                    // Disable echo for clean responses
AT+CMEE=2               // Enable verbose error messages
AT+IPR=115200           // Set UART baud rate to 115200 bps
```

| Command         | Purpose                          | Expected Response | Usage Hint                                |
|-----------------|----------------------------------|-------------------|-------------------------------------------|
| `AT`            | Check basic communication        | `OK`              | First command to test module connectivity |
| `ATE0`          | Disable command echo             | `OK`              | Send before parsing AT replies            |
| `AT+CMEE=2`     | Enable verbose error reporting   | `OK`              | Helps identify SIM/network issues         |
| `AT+IPR=115200` | Set UART baud rate to 115200 bps | `OK`              | Match baud rate on MCU/terminal side      |

> ✅ Always check responses (`OK`, `ERROR`) after each command.


## **2. SIM Card and Network Check**
Verify that the SIM card is present, unlocked, and registered on the network.

```plaintext
AT+CPIN?                // Check if SIM is ready
AT+CSQ                  // Get signal strength
AT+CREG?                // Check network registration
AT+COPS?                // Check the network operator (optional)
```

| Command         | Purpose                   | Sample Reply       | Notes                                      |
|-----------------|---------------------------|--------------------|--------------------------------------------|
| `AT+CPIN?`      | Check SIM status          | `+CPIN: READY`     | Ensure SIM is inserted and not locked      |
| `AT+CSQ`        | Signal quality            | `+CSQ: 18,0`       | RSSI >= 10 means usable signal             |
| `AT+CREG?`      | Network registration      | `+CREG: 0,1`       | 1 = Registered on home network             |
| `AT+COPS?`      | Current operator          | `+COPS: "IR-MCI"`  | Optional – useful in multi-operator areas  |

> 🔒 If SIM is locked, use `AT+CPIN="PIN"` to unlock it.


## **3. Configure Full Functionality**
Set the module to full functionality mode to enable all features like SMS, calls, and GPRS.

```plaintext
AT+CFUN=1               // Set full functionality
```

| Parameter | Meaning                        |
|---------|--------------------------------|
| `0`     | Minimum functionality (RF off) |
| `1`     | Full functionality (default)   |
| `4`     | Airplane mode (no RF)          |

> ✅ Use this command to ensure full access to cellular services.

## 4. Call Configuration
Configure the module for voice call functionality and enable caller ID.

```
AT+CLIP=1               // Enable caller ID for incoming calls
```

| Command | Purpose | Expected Response | Usage Hint |
|---------|---------|-------------------|------------|
| `AT+CLIP=1` | Show caller ID on incoming calls | `OK`, then `+CLIP` | Enables call source detection |

**Tip:** When a call comes in, expect: `RING` followed by `+CLIP: "+1234567890",145,"",,"",0`


## 5. SMS Configuration
Configure the module for sending SMS in text mode.

```
AT+CMGF=1               // Set SMS text mode
AT+CSCS="GSM"           // Use GSM character set
AT+CSMP=17,167,0,0      // SMS format parameters (MCI/MTN)
```

| Command | Purpose | Notes |
|---------|---------|-------|
| `AT+CMGF=1` | Use text mode | Easier than PDU mode |
| `AT+CSCS="GSM"` | Character encoding | Use "UCS2" for Persian/Arabic |
| `AT+CSMP=...` | SMS header/format settings | Rightel may need dcs=4 |

**Tip:** For Rightel, use `AT+CSMP=17,167,0,4`.

## 6. Clear Previous SMS
Delete stored SMS messages from memory to avoid conflicts.

```
AT+CMGD=1,4             // Delete all SMS
```

| Parameter | Meaning |
|-----------|---------|
| 0 | Delete only index |
| 1 | Delete read messages |
| 2 | Read + sent |
| 3 | Read + sent + unsent |
| 4 | Delete all messages |

**Tip:** Useful before testing new SMS functions.

## 7. Send SMS
Send an SMS message to a phone number.

```
AT+CMGS="+989123456789"
>Hello from GSM!<Ctrl+Z>
```

| Command | Description |
|---------|-------------|
| `AT+CMGS=...` | Start sending SMS |
| `<text>` | Type message body |
| `Ctrl+Z` | End message and send (ASCII 26 or 0x1A) |

**Tip:** Must be in text mode (`AT+CMGF=1`) first.

## 8. Voice Call Operations
Initiate, answer, or terminate voice calls.

```
ATD+989123456789;       // Dial a number
ATA                     // Answer an incoming call
ATH                     // Hang up an ongoing call
```

| Command | Purpose | Expected Response | Usage Hint |
|---------|---------|-------------------|------------|
| `ATD<number>;` | Dial a voice call | `OK` | Semicolon ; indicates voice call |
| `ATA` | Answer an incoming call | `OK` | When RING is received |
| `ATH` | Hang up an active or incoming call | `OK` | Ends or rejects call |

**Tip:** Ensure `AT+CFUN=1` is set to enable call functionality.

## 9. GPRS and Internet Setup
Activate internet connectivity via GPRS using the APN settings.

```
AT+QICSGP=1,"APN","",""   // Set APN (e.g., "mcinet")
AT+QIACT                  // Activate GPRS context
AT+QILOCIP                // Get local IP address
```

| Command | Purpose | Notes |
|---------|---------|-------|
| `AT+QICSGP=1,...` | Set APN credentials | Replace "APN" with carrier-specific value |
| `AT+QIACT` | Activate GPRS connection | Required before TCP/MQTT |
| `AT+QILOCIP` | Get assigned IP address | Confirm successful internet connection |

**Tip:** Example APNs:
- MCI → `mcinet`
- MTN → `mtnirancell`
- Rightel → `rightel`

## 10. MQTT Setup
Connect to an MQTT broker and authenticate.

```
AT+QMTCFG="keepalive",0,120         // Keep-alive timer
AT+QMTOPEN=0,"broker.hivemq.com",1883   // Open MQTT socket
(wait for +QMTOPEN: 0,0)

AT+QMTCONN=0,"client_id","user","pass"  // Connect client
(wait for +QMTCONN: 0,0,0)
```

| Command | Purpose | Notes |
|---------|---------|-------|
| `AT+QMTCFG=...` | Set keepalive interval | Recommended: 120 seconds |
| `AT+QMTOPEN=...` | Connect to MQTT broker | Wait for confirmation |
| `AT+QMTCONN=...` | Authenticate MQTT session | Include username/password if needed |

**Tip:** Use public brokers like `broker.hivemq.com` for testing.

## 11. MQTT Publish
After connecting to the broker, publish a message to a topic.

```
AT+QMTPUB=0,0,0,0,"sensor/temp"
> {"temperature": 25.5}<Ctrl+Z>
```

| Command | Purpose | Notes |
|---------|---------|-------|
| `AT+QMTPUB=...` | Start publishing | Enter message content after prompt |
| `Ctrl+Z` | Finish message | Ends transmission |

**Tip:** QoS can be 0, 1, or 2 depending on reliability needs.

## 12. MQTT Disconnect
Gracefully disconnect from the MQTT broker.

```
AT+QMTDISC=0                  // Disconnect MQTT session
```

| Command | Purpose | Notes |
|---------|---------|-------|
| `AT+QMTDISC=0` | Cleanly close MQTT connection | Prevent lingering sessions |

**Tip:** Always disconnect before restarting or reinitializing the module.

## 13. Summary Table

| Step | Action | Required AT Commands |
|------|--------|---------------------|
| 1 | Basic check | `AT`, `ATE0`, `AT+CMEE=2`, `AT+IPR=115200` |
| 2 | SIM & Network | `AT+CPIN?`, `AT+CSQ`, `AT+CREG?`, `AT+COPS?` |
| 3 | Full functionality | `AT+CFUN=1` |
| 4 | Call configuration | `AT+CLIP=1` |
| 5 | SMS config (optional) | `AT+CMGF=1`, `AT+CSCS="GSM"`, `AT+CSMP=...` |
| 6 | SMS cleanup (optional) | `AT+CMGD=1,4` |
| 7 | Send SMS (optional) | `AT+CMGS=...` |
| 8 | Voice call operations | `ATD<number>;`, `ATA`, `ATH` |
| 9 | GPRS setup | `AT+QICSGP=1,"APN"`, `AT+QIACT`, `AT+QILOCIP` |
| 10 | MQTT config | `AT+QMTCFG`, `AT+QMTOPEN`, `AT+QMTCONN` |
| 11 | MQTT publish | `AT+QMTPUB` |
| 12 | MQTT disconnect (optional) | `AT+QMTDISC` |

## 14. Notes

✅ **Check Responses:** Always verify responses (OK, ERROR, or specific codes like `+CREG: 0,1`) after each command.

🔧 **Module Variations:** Some modules may require slight variations (e.g., `AT+CSTT` instead of `AT+QICSGP`).

⏱ **Delays:** Add delays between critical steps (e.g., wait for `+QMTOPEN: 0,0` before proceeding).

🔄 **Flow Control:** Use hardware flow control (RTS/CTS) if supported by the module.

💾 **Save Settings:** Use `AT&W` to save configurations if supported, ensuring persistence after reboot.

📞 **Voice Calls:** Ensure the module has a microphone/speaker or headset connected for audio functionality.
