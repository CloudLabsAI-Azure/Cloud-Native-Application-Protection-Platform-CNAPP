# Module 1: Defender Cloud Security Posture Management 

### Estimated Duration: 1 Hour

## Overview
 
A hypothetical organization, "Acme Inc." had a robust cybersecurity infrastructure in place. However, one day, an attacker used a brute force or password spraying attack to gain access to an Internet-exposed server of the organization. 

The attacker could quickly move laterally through the network, exploiting vulnerabilities on the Internet-exposed servers and gaining access to the organization's Storage Accounts, SQL servers, and Key Vaults. The SOC department was alerted by Defender for Cloud on the “Brute Force, Password Spray” IOC/IOA, and quickly realized something was wrong when they noticed unusual activity on the servers and Storage Accounts. 

In response to the attack, the security engineers leveraged the attack path analysis to identify the entry point of the attack and the path the attackers used to move laterally through the network. Based on this analysis, they were able to close the entry point and cut off the attackers' access to the organization's data. 

However, the IT department didn't stop there. They also took a proactive approach by implementing security recommendations to fix the vulnerabilities on the Internet-exposed servers and prevent similar attacks in the future. They also implemented a robust incident response plan and conducted regular security training for employees to educate them on how to identify and avoid brute force and password spraying attacks. 

Thanks to the combination of both reactive and proactive measures, Acme Inc was able to prevent a major data breach and keep their sensitive information safe. This hypothetical use case demonstrates the importance of having both a reactive and proactive approach when it comes to cybersecurity, including performing attack path and security risk analysis, implementing security recommendations, assigning/managing change actions to the proper owners, and educating employees to prevent future attacks.  

Next exercise will show how to leverage the Attack Path feature of Defender for CSPM. 

## Exercise 1: Enabling Defender CSPM plan (Read Only)

In this exercise, you will learn how to enable Defender for CSPM, and leverage Defender for CSPM Capabilities

   >**Note:** To gain access to the capabilities provided by Defender CSPM, you'll need to <a href="https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-enhanced-security">enable the Defender Cloud Security Posture Management (CSPM) plan </a> on your subscription

1. In **Azure Portal**, search for **Microsoft Defender for Cloud (1)** and then click on it from the search results **(2)**. 

      ![](images/m1-img1.png)

2. From **Defender for Cloud** menu, click on **Environment Settings (1)** page and select your subscription **(2)**.

      ![](images/m1-img2.png)

3. In the **Defender plans** page, select **Defender CSPM** turn the status to **On (1)** and select **Settings & monitoring (2)**.

      ![](images/m1-img3.png)

4. Turn **On (1)** the **Agentless scanning for machines** and click **Continue (2)**.

      ![](images/m1-img4.png)

5. Click on **Save** to save the changes. 

   >**Note:** Agentless scanning for VMs provides vulnerability assessment and software inventory in 24 hours. Leave the setup and comeback after 24 hours.

      ![](images/m1-img5.png)

In this exercise, you have learnt about Enabling Defender Cloud Security Posture Management (CSPM) in Read-Only mode allows users to view and monitor security posture and compliance without making changes to settings or configurations.

## Exercise 2: Explore Attack Paths in your Environment (Read Only)

In this exercise, you will investigate and review potential attack paths in your environment in Read-Only mode to understand vulnerabilities without making changes.

1. From **Defender for Cloud** menu, open **Attack path analysis**.

    ![](./images/upimg1.png)

    >**Note:** You may not find any attack paths in your environment as we have enabled Defender CSPM recently, it will take time. As this is a read-only task just continue with further steps.

2. Click on **Attack path**. You will find the Attack Paths in your Environment. 

3. Click on **“Internet exposed VM has High severity vulnerabilities and read permission to key vault”**.

      ![](images/m1-img14.png)
 
4. You can observe the Attack path and the resources involved in the attack path.

5. Remediate the recommendations to resolve the attack path. 

6. Explore the rest of the Attack paths found in your Environment and remediate.

This exercise involves examining and reviewing potential attack paths in your environment in Read-Only mode to gain insights into security risks without altering any configurations.

## Exercise 3: Build query with Cloud Security Explorer (Read Only)

In this exercise, you will use Cloud Security Explorer in Read-Only mode to build and review queries that analyze your cloud security posture without making any modifications.

1. From **Defender for Cloud** menu, open the **Cloud Security Explorer** page.

     ![](images/m1-img6.png)
    
2. Select a predefined query Template **“Internet exposed VMs with high severity vulnerabilities” (1)** and click on **Search (2)**.

      ![](images/m1-img7.png)

3. You will find the list of VMs with high severity Vulnerabilities.

4. Select a predefined query Template **“Internet exposed SQL servers with managed identity”** and click on **Search**.

      ![](images/m1-img8.png)

5. You will find the list of SQL servers with managed identity.

6. You can also explore and build your own queries using query builder. Clear the previous query by clicking **Clear All** and **Confirm**. Next, from the dropdown select **Compute (1) -> Virtual machines (2) -> Azure Virtual Machines (3)** then click **Done (4)**. Click Search to view VMs with this vulnerability.

      ![](images/m1-img9.png)

   
 - Click on **+ (1)** and under select condition, select **Security (2)** -> **vulnerable to remote code execution (3)**.

      
      ![](images/m1-img10.png)

7. Explore your Environment for Virtual Machines with a specific vulnerability. Click on **Vulnerabilities (1)** and select **By CVE ID (2)**.

      ![](images/m1-img11.png)
 
 - Search for Virtual Machines that have a specific Vulnerability of **CVE-2021-44228** or **CVE-2021-45046**.
 
      
      ![](images/m1-img15.png)

8. Explore your Environment for Storage Accounts exposed to the Internet. From the drop-down click on **Data (1)** then select **Object storage (2)** and choose **Azure storage accounts (3)** from the list and click **Done (4)**.

      ![](images/m1-img16.png)

  - Click on **+ (1)** next to **Azure storage accounts**, then from the **Select condition** drop-down menu click on **Networking (2)** and select **Exposed to the internet (3)** and click **Search**. 

      ![](images/m1-img17.png)


9. Explore your Environment for Storage Accounts with a Sensitive Data. Change the condition to **Data (1)** and click on **Contains sensitive data (2)**.

      ![](images/m1-img18.png)

This exercise focuses on constructing and analyzing queries with Cloud Security Explorer in Read-Only mode to gain insights into cloud security data without changing configurations.

## Exercise 4: Assign Governance Rule

In this exercise, you will learn how to assign governance rules to manage and enforce compliance policies within your environment.

1. From the **Defender for Cloud** menu, click on **Environment Settings (1)** page and click on **Governance rules (2)**.

    ![](images/governance-rules.png)

2. Click on **+ Create governance rule**.

    ![](images/m1-img20.png)

3. Enter **Rule name** as `CNAPP-Rule` **(1)**, select **Scope** at subscription level **(2)** and **Priority** `100` **(3)**. Click **Next (4)**.

    ![](images/m1-img21.png)
    
4. Under **conditions** provide the below details and click **Create (5)**
	
   - **By severity**: `High` **(1)**
   - **Owner**: `By email address` **(2)**
   - **Email address**: <inject key="AzureAdUserEmail"></inject> **(3)**
   - **Remediation timeframe**: `90 days` **(4)**

    ![](images/governance-conditions.png)

5. On the **Rule created succsessfuly** pop-up select the check box next to **Apply rule to the existing recommendations that are unassigned** and click on **Ok**.

    ![](images/a1.6.png)

6. Click on **Governance report** to view the status of tasks **Complete, Ontime and Unassign**

    ![](images/governance-report.png)
    
    ![](images/m1-img24.png)

This exercise involves assigning governance rules to ensure compliance and enforce policies within your environment.

  <validation step="cd1ef464-fbfc-464e-a5ac-c4663f942da3" /> 
   
  > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
	
  - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
  - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

## Summary

In this module,you have completed essential cloud security tasks, starting with enabling the Defender CSPM plan in Read-Only mode to review security posture then exploring attack paths and potential vulnerabilities in your environment, build and analyze queries using Cloud Security Explorer, and finally, assigned governance rules to ensure compliance and effective policy management.


