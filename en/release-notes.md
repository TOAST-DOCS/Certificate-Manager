## Management > Certificate Manager > Release Notes

### March 28, 2023
#### Feature Updates
* Improved to display the message `Only files with the extension '.pem' can be uploaded.` if the selected file is not a certificate file (.pem) when registering a certificate.
* The passphrase value of the certificate is limited to a maximum of 200 characters.
#### Bug Fixes
* Fixed an issue where the Modify button is deactivated after modifying user data.

#### February 28, 2023
#### Added Features
* Added SAN certificate feature
    * SAN (subject alternative name) is a certificate that allows you to apply SSL to multiple domains with a single certificate.
    * By registering SAN certificate, you can easily manage expiration dates and notification settings for sub-certificates.
    * When you add or modify SAN certificate,  it reads information from the certificate file (.pem) to automatically enter the certificate name and sub certificate name.

#### Feature Updates
* Improved so that user data names cannot be entered only with spaces.

### January 31, 2023
#### Feature Updates
* Changed the maximum length of user data from 3,000 to 700 characters.
* Changed the naming rules for domains have.
     * The beginning and end of the domain and between dot(.) and dot(.) are limited to 63 characters.
     * The maximum length of domains is limited to 260 characters.
#### Bug Fixes
* Fixed an issue where the html format is applied when the notification group and user data names are in the html format during email notification.

### December 27, 2022
#### Feature Updates
* Improved so that, when you click the **Initialize** button on the search bar, all options are selected.
* Improved so that, even when you select a search option and close the dropdown list without clicking the **Apply** button, the selected option is applied. 
* Improved so that, when the auto-collection feature does not work in the domain, `-` is displayed on the registrar and registering institution items.
* Added an organization name to SMS notifications, and shortened guide messages.
#### Bug Fixes
Fixed an issue where, when re-entering an additional page in the domain, the expiry date is set to the previously set value.

### October 25, 2022
#### Feature Updates
* Fixed an issue where calling APIs with a project total appkey does not work properly.
* Modified the logic so that, when collection of certificates and domain information fails, mail is sent only for those confirmed that day.

### October 4, 2022
#### Feature Updates
* Fixed an issue where a permission is not properly applied when it is issued through the role group management.

### August 23, 2022
#### Feature Updates
* Changed the API's endpoint domain from api-certificate-manager.cloud.toast.com to certmanager.api.nhncloudservice.com.

### March 24, 2020
#### Added Features 
Added API to list certificates that have been added for Certificate Manager.
* [API] Added List Certificates API 

### January 21, 2020 
#### New Releases 
Certificate Manager sends alarms (via SMS or email) when you near the expiration date so that you can extend the date timely.
Certificatae Manager manages TLS certificates, domains, or user data (e.g. licenses) that have expiration dates, by specifying alarm delivery rules and recipient users.
