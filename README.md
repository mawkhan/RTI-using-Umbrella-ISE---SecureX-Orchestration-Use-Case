# Rapid-Threat-Isolation-using-Umbrella-ISE---SecureX-Orchestration-Use-Case
This workflow isolates the compromised host discovered by Umbrella at the Network layer using Cisco ISE. Cisco Umbrella is very effective when it comes to offer protection against cybersecurity threats over Internet. Cisco Umbrella can also discover already compromised systems in your Network by monitoring C2 Call-backs or BOT Call-backs happened at DNS layer.
Once Call-backs discovered, this workflow will fetch comprised system IP Address and then communicate with Cisco ISE to quarantine the End points binds to the discovered IP Address.
# Requirements:
This workflow requires following applications:
-	Cisco Umbrella ( Any package, should be integrated with Network via either Virtual Appliance or API integration with Edge devices like Cisco Routers, Meraki MX )
-	Cisco ISE
-	SecureX Remote Appliance
-	Cisco Webex ( Optional, for receiving alerts about the threat )
-	AMP4E ( Optional , for casebooks, threat response )

# Workflow Steps:
-	Fetch global variables
-	Fetch last alert from Cisco Umbrella
-	Extract observations from the last alert
-	For last alert:
Check if the alert is new by comparing the latest alert time saved in global variable
If it was:
   
     If comprised device is internal:
             - Communicate with Cisco ISE to isolate the observed IP from the alert
             - Update the global variables with the value of current alert time
             - Post a Webex team message with summary and link to investigate further
     If it is external:
             - Post a Webex team message with summary and link to investigate further

If it wasn’t:
             -  Update the global variables with the value of current alert time
# Configuration Steps:
-	Setting up the SecureX Remote Connector by installing it on-premise Network by following steps mention at below link:
https://ciscosecurity.github.io/sxo-05-security-workflows/remote
![1](https://user-images.githubusercontent.com/86117124/141064011-a50c3ec2-a24c-406a-930f-60924ce1dce5.png)
-	Make sure SecureX remote is reachable from ISE
-	Setting up Account Keys in Secure X
-	Setting up Target for ISE which should include remote connector & account keys
![2](https://user-images.githubusercontent.com/86117124/141064044-9ae90c32-ab06-45fe-896b-2c62abde653f.png)
![3](https://user-images.githubusercontent.com/86117124/141064052-bd6e98f1-c064-47c6-9b35-c8d7ff2b5200.png)
-	Import the workflow code. Goto file name"code" in this repository, it is json formatted code which need to be copied and then paste in SecureX Orcuestration. 
![4](https://user-images.githubusercontent.com/86117124/141064061-25e83821-3ad9-4a22-933b-63af7546064f.png)
-	Setting up the variables as listed below:
![5](https://user-images.githubusercontent.com/86117124/141065976-b5607f19-9548-4d3e-8f98-8b480c4d084d.png)
![6](https://user-images.githubusercontent.com/86117124/141065988-42cfa8a1-c80e-4d42-8e4a-f560ad41077e.png)
-	Setting up the ISE Targets as shown below:
![7](https://user-images.githubusercontent.com/86117124/141064093-b57e8be1-826f-4b0d-87ce-0584842e7827.png)
-	Make sure trigger is attached to the workflow and enabled
-	Click on validated
![9](https://user-images.githubusercontent.com/86117124/141064115-ea3a8808-ab09-4090-93c4-f3038cdb9bbe.png)

# Verification:
-	Check trigger is started
![10](https://user-images.githubusercontent.com/86117124/141064127-cba4b7ed-54bf-49c2-92cf-ad3f201281b2.png)
-	Click on view runs to check whether workflow is running  constantly 
![11](https://user-images.githubusercontent.com/86117124/141064129-51e2a9f6-85c3-47c4-b01e-6269231d0c3c.png)
-	Open a url https://www.examplebotnetdomain.com
-	You should receive message on webex and case will be created inside secureX casebook
![13](https://user-images.githubusercontent.com/86117124/141067823-ec3a5975-3f63-49e8-9a85-add0ca40732e.png)

# Links to DevNet Learning Labs
[SecureX Orchestration](https://developer.cisco.com/learning/modules/SecureX-orchestration)
