# automated wi-fi credential theft leveraging the flipper zero

## The Dangers of Automated Wi-Fi Credential Theft: A Look at Exploitative Scripting

We connect our devices seamlessly to Wi-Fi networks, often unaware of the security risks lurking beneath. One such danger is the use of malicious scripts that exploit system vulnerabilities to steal sensitive Wi-Fi credentials. This script, when deployed maliciously, highlights how easily Wi-Fi credentials can be extracted and exfiltrated.

## What Does This Script Do?

This PowerShell-based DuckyScript automates the process of extracting Wi-Fi credentials stored on a Windows machine and sending them to a specified Discord webhook. The script uses the following steps:
  1. **Accessing Wi-Fi Profiles:** It retrieves all Wi-Fi profiles stored on the machine using the netsh wlan show profiles command.
  2. **Extracting Passwords:** For each Wi-Fi profile, it runs a command (netsh wlan show profile name="<profile>" key=clear) to reveal the saved Wi-Fi password (if one         exists).
  3. **Sending Data to a Discord Webhook:** The extracted Wi-Fi profile names and passwords are packaged into JSON format and sent to a Discord webhook using                    Invoke-RestMethod.

In the hands of an attacker, this script can easily steal Wi-Fi passwords from a victim’s machine without their knowledge.

## Why This Is Dangerous

  1. **Wi-Fi Credential Theft:** Once an attacker gains access to Wi-Fi credentials, they have the ability to connect to that network at any time. This could lead to:

       **Man-in-the-middle attacks:** If the Wi-Fi network is unencrypted or poorly secured, an attacker can intercept sensitive data transmitted over the network, such             as banking information, login credentials, or personal communications.

       **Network exploitation:** An attacker with access to the network can scan for vulnerable devices, infect machines with malware, and compromise other network                  resources.
  3. **Wide Attack Surface:** In large organizations or households with multiple Wi-Fi networks and devices, an attacker can extract all stored network credentials. Even          if one network is secure, another one may not be, giving the attacker multiple entry points to the same environment.
  4. **Abuse of Discord Webhooks:** Discord webhooks allow developers and users to send messages automatically to Discord channels. However, attackers can exploit webhooks        as an easy way to exfiltrate data without raising suspicion. Since Discord is commonly used for gaming and communication, this method may go unnoticed for longer           periods.
  5. **Unnoticeable Execution:** DuckyScripts, like the one presented, are often deployed through USB Rubber Ducky devices, which can execute commands rapidly and without         user intervention. By mimicking legitimate input, the script can be run without triggering antivirus or other security tools.

## Why This Script Is a Red Flag

  1. **Undetected Execution**  The script runs silently, with no visible indicators for the user. It leverages tools native to the Windows operating system (PowerShell and        netsh), so it can evade detection by traditional antivirus software unless the system is monitored closely.
  2. **Web-based Exfiltration:** Using a Discord webhook for exfiltrating data ensures that the data is quickly and efficiently sent to an external server (Discord) with          minimal chance of detection, as Discord traffic is unlikely to be flagged by most firewalls or network monitoring tools.

## Preventing Exploitation

  1. **Limit Access to Wi-Fi Profiles:** Ensure that only trusted devices have access to Wi-Fi profiles on your network. This minimizes the risk of someone physically             connecting a malicious device and executing scripts like this one.
  2. **Monitor Webhook Activity:** Organizations should closely monitor traffic to popular communication platforms like Discord. Any unexpected activity could indicate            that data is being exfiltrated via webhooks.
  3. **Harden PowerShell Security:** PowerShell is a powerful tool, but it can also be exploited by attackers. Organizations should enable logging and auditing for                PowerShell scripts to detect any malicious use. Also, consider using AppLocker or Device Guard to restrict the execution of unapproved scripts.
  4. **Educate Users:** Awareness and training go a long way. Users should be informed of the risks of inserting untrusted USB devices into their machines, as USB Rubber          Ducky devices can easily mimic keyboards and run scripts like this one.

## Disclaimer
***This script is intended strictly for educational and testing of approved targets only.  Sasquatchchicken is not responsible for any misuse of the provided script.          Always act in accordance of the law***

