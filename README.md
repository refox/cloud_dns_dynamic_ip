# Overview
The script [update_dynamic_ip.py] is designed to manage syncing the external IP address (that is, the IP address the world sees, as viewed from myexternalip.com) of the machine the script is run on with a Google Cloud DNS managed zone.

# Requirements
* python with httplib2, google-api-python-client and pyopenssl
* Google Cloud Platform Project (with [CloudDNS](https://developers.google.com/cloud-dns/getting-started) enabled)
* Valid service account secrets file ([instructions](https://developers.google.com/api-client-library/python/guide/aaa_oauth#acquiring))
  * The downloaded file must be converted with 'openssl pkcs12 -in project.p12 -nodes -nocerts > privatekey.pem'.

# Getting Started

* Schedule the script to run (cron)

# Usage
usage: update_dynamic_ip.py client_email project_name zone sub_domain

# Program Flow
* List all records in the managed zone
  * Check that there is an SOA record
  * Check if there is an existing sub-domain record
* Query for external ip address from myexternalip.com
* Check to see if our ip has changed
* Create a new SOA record (with increased serial number)
* Create new A record for the given subdomain
* Send change request
