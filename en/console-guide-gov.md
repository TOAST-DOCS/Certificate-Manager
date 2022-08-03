## Management > Certificate Manager > Console User Guide 
Console User Guide describes basic requirements to enable Certificate Manager. 
* Notification Group
* Certificate
* Domain
* User Data 

## Notification Group

Certificate Manager sets notification cycle on each expiration date and manages notification recipients, by notification group.  

![alarmgroup-1.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-1.png)

### Creating Notification Groups

1. Click **+ Create Groups** on the main page of notification group, and you'll find a page like below. 
![alarmgroup-2.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-2.png)
2. Enter name for a group. No duplicate name is allowed. 
3. Enter whether to enable notification. You can choose whether to send all notifications, including expiration dates, to group users. 
4. Click **Add** and create a notification group. 

### Detail Page

1. Click **Details** on the main page, and it shows name of the group, whether notification is enabled, and management data. **Managed Data** refers to certificate/domain/user data that are integrated with each notification group. 
2. Click **Edit** to change name of the group or notification enabled/disabled.    

![alarmgroup-3.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-3.png)

### Notification Setup

1. Click **Notification Setting** on the main page and you can find notification policy for expiration dates set for each notification group. 
2. By default, notification policy is not set. You need to add notification policy to be notified on each expiration date. ![alarmgroup-4.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-4.png)

### Adding Notifications

1. Click **+** at the bottom left of the table to add notification policy. ![alarmgroup-5.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-5.png) 
2. **D-day for Notification Start** refers to since how many days ago notifications can be sent from expiration dates of certificate/domain/user data. 
3. **Notification Cycle** means how often notification is to be sent from D-day for notification start. 
4. **Send via Email** and **Send via SMS** refer to whether to use Email or SMS to send notifications. If both are unchecked, notification is not sent. 
5. Click **-** of **Delete** to delete notification policy. 
6. **D-day for Notification Start** and **Notification Cycle** cannot be redundantly set. 
7. Click **Completed** to save notification policy as configured. 
![alarmgroup-6.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-6.png)

### User Group Integration

On the main page of notification group, click **Receiving group**, and users that are integrated to the notification group are displayed. 
By default, the notification group creator is added. 

NHN Cloud project members can be integrated as the group users. ![alarmgroup-7.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-7.png)

### Adding Users

On the search window for user integration above, you may search and add NHN Cloud project members.

![alarmgroup-8.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-8.png)
![alarmgroup-9.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-9.png)
  
* **Type** refers to the user's authority (Admin/Member) for a NHN Cloud project. 
* You can check **Name**, **Email** and **Phone** of each member. 
* When a member's mobile phone number is not registered, you shall find '-' for **Phone**. In such case, it fails to send notification via SMS; then, a failure message of notification delivery is sent to ADMIN of each group.   

## Certificate

Enter domain name (e.g. *.toast.com) and expiration date of certificate, and then notification is sent to user, in accordance with notification policy of an integrated notification group.
 
To upload certificate files (.pem), following items are automatically collected from such files. 
* Creation date
* Expiration date
* Signature type of a certificate (ex: sha256RSA)
* Certification institution (ex. Digicert)

To register certificate installation information, import certificate from the IP and port of such information so as to compare them with registered certificate and expiration date at CertificateManager. 
If auto-collected certificate installation information has earlier expiration date than that of the registered certificate at CertificateManager, notification is sent to alert that certificate needs to be replaced. 

### Main Page
On the main page of certificate, you can find list of certificates and remaining days until expired.

![certificate-1.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-1.png)

* You can find and search the list of already registered certificates. 
* Also check remaining days until expired. 
* As of today, expired data are displayed in red, whereas data with less than 30 days until expired are displayed in orange.  

### Creating Certificates

1. On the main page of a certificate, click **+ Add Certificates** and you can find the page as follows. 
![certificate-2.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-2.png)
2. Select a **Notification Group** to integrate. In case a notification group is not created, there is no available notification group, and hence certificate cannot be created. 
3. Enter **Name** of a certificate (CommonName, CN): names cannot be redundantly registered. 
4. Select **Type**. Single refers to a single certificate, while Wildcard is a common-purpose certificate (available for many hosts) starting with *(asterisk). 
5. Register a certificate file.<br>
Certificate file is an optional field, and you may skip it for later. 
    * A certificate (.pem) is a pem file comprised of a private key and a certificate. 
    * For supported type of certificate file (.pem), see '[Troubleshooting Guide > Converting Certificate File Formats](http://gov-docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)'.
    * The maximum uploadable certificate is 512KB. 
6. Enter **Passphrase** of the private key included within certificate file. 
7. Click **Add** to save certificate information as configured. 
8. In order to integrate with [Network > Load Balancer](https://gov.toast.com/kr/service/network/load-balancer), passphrase of the certificate file must be deleted. 
    * Use the following command to delete passphrase. 
    ```bash
    openssl rsa -in my_private_input.key -out my_private_output.key
    ```

### Detail Page

1. Click **Details** on the main page of a certificate to find information of the certificate and file. 
    * Fields specified as **(Auto Collect)** after field name refer to automatically collected items from certificate files. If there is no registered certificate file, '-' shows.  
2. Click **Edit** to modify certificate information or (re)upload certificate files. 
    * Certificate names cannot be edited. If a name must be edited, delete a registered certificate and create a new one. 
    ![certificate-3.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-3.png)

### Creating Certificate Usage/Installation Information

1. Click **Certificate Usages** on the main page, and find usage and installation information of certificate. By default, no item is registered. 
![certificate-4.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-4.png)
2. Click **Edit** to find a page as below. 
![certificate-5.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-5.png)
3. Click **+ Add** on top right to show a window to register certificate usage information. 
![certificate-6.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-6.png))
4. Enter name for certificate usage information. 
    * If the certificate type is **Single**, the name must be same as certificate name. 
    * If the certificate type is **Wildcard**, the name must be same as certificate name, excluding '\*'(asterisk), or must end with ".[Certificate Name]", excluding  '\*'(asterisk). 
5. Enter whether to enable notification for certificate usage information.
6. To enter certificate installation information, click **+ Add** next to Certificate Installation Information. Then, a window like below shows. 
![certificate-7.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-7.png)
    * Enter **IP address** and **Port No.**. When auto-collect is enabled, download certificate via IP address and port number to compare expiration dates. 
    * In case of a private IP address (e.g. 192.168.0.1, 172.20.0.1, 10.0.0.1 ), downloading may fail and notification on failed auto collection may be sent.  
7. Click **Completed** to save usage and installation information of the certificate as set. 

### Page of Certificate Usage Information
* On the main page of a certificate, click **Certificate Usages** to check usage and installation information of certificate. 
* Notifications of usage information can be filtered by selecting **Total**, **Enabled**, or **Not Use** on top right.  

![certificate-8.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-8.png)

## Domain
Enter name of domain (the highest domain name of DNS, e.g. toast.com) and expiration date, and notifications are sent to users in accordance with notification policy of an integrated notification group.
 
If 'Auto Collect' is enabled for domain, domain information is automatically collected from the whois server. 
Following items are automatically collected:
* Creation Date
* Expiration Date
* Registrar (ex.Gabia, Inc.)
* Registration institution (Registrant, domain's real owner) 
* Name server 

### Main Page

You can find and search the list of already registered domains.

![domain-1.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-1.png)
 
Also check remaining days until expired. 

As of today, expired data are displayed in red, whereas data with less than 30 days until expired are displayed in orange. 

### Creating Domains

1. On the main page of a domain, click **+ Add Domains** and you can find the page as follows. 
![domain-2.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-2.png)
2. Select a notification group to integrate. In case a notification group is not created, there is no available notification group, and hence domain cannot be created. 
3. Enter **Name** of a upper domain: upper domain names cannot be redundantly registered. 
4. Enter **Date of expiration** of the domain.
5. Select **Type**.
    * **For Service** refers to registering and using domains on a DNS server
    * while **For Defense** refers to acquiring by purchase of domain for the purpose of service credibility, although it is not practically applied. 
6. Select whether to enable notifications. It shows whether to send notifications to each domain, and with **Not Use**, no notification is sent to the corresponding domain. 
7. Select to enable/disable **Auto Collect**. If Auto Collect is **Enable**, following items are automatically collected from the whois server:
    * Creation Date
    * Expiration Date
    * Registrar (ex.Gabia, Inc.)
    * Registration institution (Registrant, domain's real owner) 
    * Name server 
8. Enter whether to auto-collect sub-domain and name of the domain. 
    * With auto-collect enabled, call ping to the corresponding domain to check if it gets response successfully. 
    * A sub-domain name must belong to a upper domain. 
        * Name of a sub-domain must be same as that of a upper domain, or end with "[Name of Upper Domain]".
        * ex. If a upper domain is named "toast.com", a sub-domain can be named as "toast.com", "www.toast.com", or "www2.toast.com".
9. Click **Add** to save domain information as configured. 

### Detail Page

1. Click **Detail Information** on the main page of a domain to find information of the domain and sub-domain and file. 
2. Fields specified as **(Auto Collect)** after field name refer to automatically collected items. If there is no automatically collected information, '-' shows.  
3. Click **Edit** to modify upper domain information, delete a registered sub-domain or add a sub-domain.   
    * Upper domain names cannot be edited. If a name must be edited, delete a registered domain and create a new one. 

![domain-3.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-3.png)

## User Data

Enter data with expiration dates (e.g. license key) and notifications are sent to users in accordance with notification policy of an integrated notification group.  
This feature is applicable when notification is required on a regular basis to specific user groups. 

### Main Page

You can find and search the list of already registered certificates. Also check remaining days until expired. 
As of today, expired data are displayed in red, whereas data with less than 30 days until expired are displayed in orange.

![userdata-1.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-1.png) 

### Creating User Data

Click **+ Add User Data** on the main user data page and it shows the following. 

![userdata-2.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-2.png)

* Select a notification group to integrate. In case a notification group is not created, there is no available notification group, and hence user data cannot be created. 
* Enter name of user data: user data name cannot be redundantly registered.  Enter name of user data: user data names cannot be redundantly registered. 
* Select whether to send notification, which refers to whether to send notifications on corresponding user data. With **Not Use**, no notification is sent regarding the user data.  
* Enter expiration date of the user data. 
* Click **Add** and save user data as configured. 

### Detail Page

Click **Details** on the main user data page, and user data information as saved shows up. 

Click **Edit** to edit user data information. 

![userdata-3.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-3.png)
