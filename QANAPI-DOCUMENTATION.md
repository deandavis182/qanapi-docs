---
title: Qanapi User Documentation
description: 'A detailed guide on how to navigate and use Qanapi'
---

# **Qanapi User Documentation**

## **Overview**

Qanapi is an advanced API-based encryption service designed to provide granular control over your sensitive data. As a third-party key management service, Qanapi enables organizations to encrypt and decrypt data with ease, while securely managing encryption keys. It offers robust data classification features, allowing you to control who can access specific parts of your data based on classifications and access groups.

This documentation provides a detailed guide on how to navigate and use the Qanapi web app/dashboard. The following sections will guide you through the registration process, navigating the dashboard, managing projects, configuring settings, and managing your account.

### **Sections Covered:**

1. [Registration Process](#registration-process)
2. [Navigating the Dashboard and Creating a New Project](#navigating-the-dashboard-and-creating-a-new-project)
3. [Project Overview and Management](#project-overview-and-management)
4. [Team Management](#team-management)
5. [Billing Management](#billing-management)
6. [Security Log](#security-log)
7. [Application Settings](#application-settings)
8. [Using Templates](#using-templates)
9. [My Account](#my-account)

---

## **Registration Process**

To begin using the Qanapi web app/dashboard, you need to create a new account. Follow these steps to register:

### **Access the Registration Page:**

* Visit the registration page by navigating to [https://kbosscloud.com/register/](https://kbosscloud.com/register/).

### **Fill Out the Registration Form:**

* **Company:** Enter the name of your company in the "Company" field.  
* **Full Name:** Provide your full name in the "Full name" field.  
* **Domain:** Choose a unique subdomain for your tenant instance. This subdomain will be followed by `.kbosscloud.com`. The domain can only contain lowercase letters with no numbers or special characters.  
* **Email Address:** Enter your business email address.  
* **Password:** Create a secure password.  
* **Confirm Password:** Re-enter the password to confirm it.

### **Agree to the Terms of Service:**

* Check the box to agree to the Terms of Service before proceeding.

### **Create Account:**

* Once all fields are completed, click the **Create Account** button to submit your information.

**Note:** By creating an account, you acknowledge that the system is subject to U.S. government information regulations. Be sure to review the legal notice at the bottom of the page.

After successfully submitting the form, a tenant instance will be created, and you will be redirected to your tenant's subdomain, where you can start configuring your dashboard.

---

## **Navigating the Dashboard and Creating a New Project**

After successfully registering and logging into your tenant's Qanapi dashboard, you'll be greeted with the Projects page. Here’s how to navigate and create your first project.

### **Projects Page**

Upon logging in, you’ll be directed to the `/projects` page. This page displays all the projects you've created, which is initially empty. To get started, follow these steps:

### **Navigating to the Projects Page:**

* In the left-hand sidebar, click on **Projects** to view and manage your projects.

### **Creating a New Project:**

* To create a new project, click on the **New Project** button located in the center of the Projects page.

### **Creating a New Project \- Popout Form**

Once you click on **New Project**, a popout form will appear where you can configure the details of your new project.

* **Project Name:** Enter a unique name for your project in the "Project name" field (e.g., "Example project").  
* **Environment:** Select the appropriate environment from the "Environment" dropdown. Options may include "Development," "Staging," or "Production." Note that environments cannot be modified after creation.  
* **Datacenter:** Choose the datacenter where your project data will be stored. For example, "GCP us-central1 (Council Bluffs, Iowa)".  
* **Qanapi Engine Configuration:**  
  * **Cloud (Fully Managed):** The default option where Qanapi manages the infrastructure.  
  * **Custom:** If selected, you can enter a Fully Qualified Domain Name (FQDN) or IP address where you want the Qanapi engine to be configured.  
* **Encryption Strategy:**  
  * **AES-256:** FIPS 140-2 and quantum-resistant, Symmetric encryption.  
  * **RSA-2048:** Quantum-resistant and BYO key, Asymmetric encryption.  
  * **RSA-4096:** Quantum-resistant and BYO key, Asymmetric encryption.  
* **Additional Functions:**  
  * **Cloud HSM:** Toggle this option if you want your master key to be managed using a Hardware Security Module (HSM).  
  * **Malicious Payload Scanning:** This option is enabled by default, scanning data for malicious content.  
  * **AI Content Detection:** Detects AI-generated content.  
  * **AI Insights:** Provides transaction insights using the Llama 2 model.  
* **Create Project:** After filling out all the necessary fields, click the **Create** button to finalize and create your new project.

---

## **Project Overview and Management**

### **Project Overview**

After creating a new project, you are directed to the **Project Overview** page. This page provides a step-by-step guide to help you configure your project:

### **Project Configuration Steps:**

* **Create Project:** You've already configured your new Qanapi project.  
* **Create an API Key:** API keys allow you to use the Qanapi API.  
* **Create Data Classifications:** Choose your data classifications to associate them with your sensitive data.  
* **Data Proxies:** Use the Data Proxy to easily encrypt and forward HTTP requests.

### **API Keys**

The **API Keys** tab allows you to create and manage API keys for your project.

#### **Creating an API Key:**

* Navigate to the **API Keys** tab.  
* Click on the **Create API Key** button.  
* A prompt will appear, notifying you that the API key will only be displayed once and will be irretrievable after it is shown. Ensure you store this key securely.  
* Click **Create API Key** to generate a new key. The key will be listed under the **API Keys** section.

### **Data Proxies**

The **Data Proxies** tab is where you find the endpoint URL specific to your project for encrypting and decrypting data.

#### **Smart Data Proxies:**

* The Data Proxy provides a powerful HTTP endpoint that allows you to seamlessly encrypt, classify, and protect data within any HTTP request, ensuring that sensitive data is never exposed to the destination.  
* The proxy details, including the environment (e.g., Development) and the specific URL for the data proxy, are displayed here.
* Requests forwarded to the destination use the same HTTP method (GET, POST, etc.) and headers as the original request. The body of the request is encrypted and classified using the Qanapi platform, and the destination URL is protected from seeing the sensitive data.  
* An example cURL command is provided, illustrating how to use the Data Proxy for encryption and classification in a request.

#### **Using the Smart Data Proxy for Encryption and Decryption:**

**Required Headers**

- **`X-KBOSS-Authorization`**: Your API authorization token.
- **`x-kboss-mode`**: Specify `encrypt` for encryption and `decrypt` for decryption.
- **`X-KBOSS-Fields`**: Comma-separated list of fields in the JSON payload to be encrypted or decrypted.
- **`Content-Type`**: Set to `application/json` for JSON payloads.

**Optional Headers**

- **`X-KBOSS-Destination`**: A URL to forward the request to after encryption instead of returning the encrypted data to the client. This is useful for workflows where the encrypted data needs to be sent to another service.
- **`X-KBOSS-Classification`**: The classification level of the data (e.g., `cui`, `health`, `financial`).


#### **Encrypting Data**

Below is an example of how to use the Smart Data Proxy to encrypt data.

```bash
curl --location 'https://customer-subdomain.kbosscloud.com/proxy/xxxxxxx' \
--header 'X-KBOSS-Authorization: cd_xxxxxxxxxxxxxxxxxx' \
--header 'x-kboss-mode: encrypt' \
--header 'X-KBOSS-Fields: title,body' \
--header 'X-KBOSS-Classification: cui' \
--header 'Content-Type: application/json' \
--data '{
    "userId": 1,
    "id": 1,
    "title": "Title text to encrypt",
    "body": "Bunch of Body text to encrypt"
}'
```

#### **Decrypting Data**

Below is an example of how to use the Smart Data Proxy to decrypt data.

```bash
curl --location 'https://customer-subdomain.kbosscloud.com/proxy/xxxxxxx' \
--header 'X-KBOSS-Authorization: cd_xxxxxxxxxxxxxxxxxx' \
--header 'x-kboss-mode: decrypt' \
--header 'X-KBOSS-Fields: title,body' \
--header 'X-KBOSS-Classification: cui' \
--header 'Content-Type: application/json' \
--data '{
  "userId":1,
  "id":1,
  "title":"kboss:bm9uZQ:MDFqNDRrZmJmenkyc3ZqbTg1NG5qYng2d2c:dHFkY1Q1MW81Y1hLcTRCdkxibG1DK3NoMnF0ZFE3OFVIa3REbFZwVGpmQT0:$",
  "body":"kboss:bm9uZQ:MDFqNDRrZmJnOWN4ejYwcHFxOWo3c3huYXE:dzlTdlYwVkNVK0xmVXUwM2JLT2xGQi9rbHF4R1l0MWxCZlR5QlNqeHpZUT0:$"
}'
```

#### **Forwarding Encrypted Data**

To forward the encrypted data to another service, use the `X-KBOSS-Destination` header with the desired destination URL.

```bash
curl --location 'https://customer-subdomain.kbosscloud.com/proxy/xxxxxxx' \
--header 'X-KBOSS-Authorization: cd_xxxxxxxxxxxxxxxxxx' \
--header 'x-kboss-mode: encrypt' \
--header 'X-KBOSS-Fields: title,body' \
--header 'X-KBOSS-Classification: cui' \
--header 'X-KBOSS-Destination: https://example.com/receive-encrypted-data' \
--header 'Content-Type: application/json' \
--data '{
    "userId": 1,
    "id": 1,
    "title": "Title text to encrypt",
    "body": "Bunch of Body text to encrypt"
}'
```

### **Data Classifications**

In the **Classifications** tab, you can create and manage data classification tags to associate with your encrypted data.

#### **Creating a Classification Tag:**

* Click the **Create Classification** button.  
* Fill in the details:  
  * **Name:** Enter a name for the classification tag (e.g., Health, Commercial, CUI).  
  * **Description:** Optionally, provide a description that will be used within system-generated compliance documentation.  
  * **Background Color and Text Color:** You can customize the colors for the tag, which may be used in third-party applications (e.g., text highlighting).  
* Click **Create** to finalize the classification tag.

### **Log Destinations**

The **Log Destinations** tab allows you to configure where the logs for your project should be sent.

#### **Configuring Log Destinations:**

* You can connect your project to a SIEM tool by configuring one of the available connectors:  
  * **Splunk Connector:** Send events to your Splunk Cloud or Splunk Enterprise service.  
  * **Google Cloud Logging:** Send events to Google Cloud Logging, which can be ingested into Google Chronicle for SIEM functionality.  
  * **Exabeam Connector:** (Coming Soon) Send events to your Exabeam service.

### **Event Log**

The **Event Log** tab displays all events related to your project.

#### **Viewing Events:**

* This section lists the latest events related to your project. If no events have occurred, the section will indicate that there are currently no events to display.

---

## **Team Management**

### **Team Management**

The **Team** tab in the Qanapi dashboard allows you to manage team members who have access to your organization’s Qanapi environment.

#### **Viewing Team Members:**

* The **Team Management** page lists all current members of your team, including their User ID, Name, Email, and Join Date.

#### **Inviting a New Team Member:**

* To add a new team member, click the **Invite team member** button.  
* You can enter the new member's email address and send them an invitation to join your Qanapi environment.

---

## **Billing Management**

### **Billing Management**

The **Billing** tab allows you to manage your organization’s subscription, payment methods, and invoices.

#### **Subscription Details:**

* The billing page will display your trial end date, if applicable, and provide options to upgrade to a PRO account.  
* Click the **Upgrade** button to select a subscription plan.

#### **Sharing Billing Information:**

* You can share a billing link with someone else by copying the link provided under the "Share this link" section. This allows another person to complete the checkout on your behalf.

#### **Upcoming Payments and Invoices:**

* The billing page will also display information about upcoming payments and issued invoices once you subscribe to a plan.

---

## **Security Log**

### **Security Log**

The **Security Log** tab provides a detailed history of actions taken within your Qanapi environment.

#### **Viewing Security Events:**

* The security log lists actions taken by users, such as logins, including details like IP address, timestamp, and action performed.

---

## **Application Settings**

### **Application Settings**

The **Settings** tab allows you to configure various aspects of your Qanapi application, including domains and company information.

#### **Configuration:**

* **Company Name:** Update your company name in the **Company name** field and click **Save** to apply the changes.

#### **Domains:**

* Manage your application's domains under the **Domains** section.  
  * **Add a Custom Domain:** You can add a custom domain by entering the domain name and clicking **Save**. An SSL certificate will be generated automatically after DNS has been updated, which may take some time.  
  * **Fallback Subdomain:** Change the fallback subdomain for your application if it does not have a custom domain. Be aware that changing this subdomain may affect your users, and you should notify them of any URL changes.

---

## **Using Templates**

### **Using Templates**

The **Templates** tab provides pre-configured quickstart templates that help you integrate Qanapi with popular cloud services.

#### **Quickstart Templates:**

* The templates page offers various integration templates, such as Atlassian Confluence, Jira, Monday.com, Workday, Asana, Stripe, Salesforce, and more.  
* Select a template by clicking **Start building** next to the desired service.

#### **Getting Started with a Template:**

* Click on **Get started** at the top of the templates page to begin the integration process using Qanapi's proprietary AI model. This model generates secure, compliant code to integrate encryption and security services into your applications quickly and easily.

---

## **My Account**

### **Accessing My Account**

To manage your personal account settings in Qanapi:

#### **Navigate to My Account:**

* Click on your username in the top-right corner of the Qanapi dashboard.  
* From the drop-down menu, select **Profile** to access your account settings.

### **Personal Information**

The **My Account** page allows you to update your personal information and manage your password.

#### **Updating Personal Information:**

* **Name:** Your name is displayed in the "Name" field. You can update it as needed.  
* **Email Address:** Your email address is displayed in the "Email address" field. If you need to change your email, update the field and click **Save** to apply the changes.

### **Password Management**

#### **Changing Your Password:**

* **Current Password:** Your current password is required to make any changes.  
* **New Password:** Enter a new password in the "New password" field.  
* **Confirm Password:** Re-enter the new password to confirm.  
* Click **Save** to apply the changes to your password.

