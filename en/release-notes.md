## Management > Certificate Manager > Release Notes

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
