# Tines_Crowdstrike
source article: https://www.tines.com/blog/getting-connected-to-the-crowdstrike-api/


When working with any API, some common initial considerations include:

Documentation: Where can I find it, and how comprehensive is it?
Endpoints: What specific endpoints are available?
Authentication: How do I authenticate?
Prerequisites and Limitations: Are there any setup requirements, restrictions, or potential challenges?
Tooling: What tools can I use for quick prototyping and testing?
CrowdStrike API Documentation
Access to CrowdStrike's API documentation requires you to be logged in via the web. Note that documentation links vary by your cloud environment (US-1, US-2, US-GOV-1, EU-1) and will match your login URL’s hostname pattern.

Main Documentation: Link
REST API User Manual: Focuses on the OAuth2.0-based authentication model (legacy key-based authentication is deprecated).
REST API Reference Documentation (Swagger/OpenAPI):
US-1: Swagger API Reference
US-2: Swagger API Reference
US-GOV-1: Swagger API Reference
EU-1: Swagger API Reference
Support Portal: Requires entitlement to access.
API Endpoints
Your account type determines the endpoint to use:

US-1: api.crowdstrike.com
US-2: api.us-2.crowdstrike.com
US-GOV-1: api.laggar.gcw.crowdstrike.com
EU-1: api.eu-1.crowdstrike.com
API Authentication
CrowdStrike supports OAuth2.0 authentication. While key-based authentication is available, it is deprecated and not recommended.

API Limitations
Each API call response includes rate-limiting metrics:

x-ratelimit-limit: Max allowed calls per minute.
x-ratelimit-remaining: Remaining calls allowed in the time window.
x-rateLimit-retryafter (optional): UTC epoch timestamp indicating when at least one request will be available if you exceed your limit.
Tooling
For testing APIs:

cURL: A quick command-line tool but can be cumbersome with OAuth2.0 parameters.
Postman: A versatile option for API testing.
Tines: Preferred for its native OAuth2.0 support, simplifying token generation, usage, and renewal.
Quick Setup Guide

Step 1: Generate CrowdStrike Client Key and Secret
Log in to the Falcon platform with admin access.
Navigate to Support > API Clients and Keys > Add New API Client.
Provide a name, description, and allocate required scopes (e.g., read permissions across all endpoints).
Upon confirmation, store the generated Client ID and Secret securely.
![image](https://github.com/user-attachments/assets/eda4229e-9d62-456d-b8f5-36dca4252c49)

Step 2: Create CrowdStrike Credentials in Tines
Go to Credentials in Tines and click + New Credential.
Use the following settings:
Type: OAuth2.0
Credential Name: CrowdStrike
Callback URL: https://<your_tines_tenant_name>.tines.io/oauth2/callback
Client ID: (from Step 1)
Client Secret: (from Step 1)
Scope: Read Write
Grant Type: client_credentials
OAuth Authorization Request URL: https://api.us-2.crowdstrike.com/oauth2/token
OAuth Token URL: https://api.us-2.crowdstrike.com/oauth2/token


Step 3: Define CrowdStrike API Resource in Tines
Navigate to Resources and click + New Resource.
Create a resource with:
Name: crowdstrike_domain
Builder (text): us-2.crowdstrike.com
This will generate a shortcode {{ RESOURCE.crowdstrike_domain }} for reuse.

Step 4: Implement Credentials in a Tines Action
Create a new Tines Story and drag a CrowdStrike Action (e.g., Get Detections in CrowdStrike Falcon) onto the storyboard.
Adjust the Action properties:
Use {{ global_resource crowdstrike_api }} for the domain.
Use {{ credential crowdstrike }} for credentials.
Run the action and verify the results in the Events tab.
![image](https://github.com/user-attachments/assets/01b7c961-ca09-43a0-9ef4-ff125ee75503)
![image](https://github.com/user-attachments/assets/10123c65-393e-4aa4-b17b-b73c67a43b71)
![image](https://github.com/user-attachments/assets/71b4877c-a2aa-4728-aada-c09dc2981443)
![image](https://github.com/user-attachments/assets/0ac5328d-f7f6-48aa-a41a-78dc5a344f47)

