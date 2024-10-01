# Exercise 02: Defender for Containers

### Estimated Duration: 90 minutes

Microsoft Defender for Containers is a comprehensive security solution designed to protect containerized applications throughout their lifecycle, from development to production. It offers a robust set of features that help secure both the container images and the orchestration platforms, such as Kubernetes. By integrating seamlessly with Azure services and popular container tools, Defender for Containers provides continuous threat detection, vulnerability management, and runtime protection. Its ability to monitor container environments in real-time enables organizations to identify and respond to threats quickly, ensuring the security of their cloud-native applications.

For example, consider a software development company that deploys a microservices architecture using Kubernetes. As developers create and deploy containerized applications, they often use various open-source libraries and frameworks. Defender for Containers scans these images for vulnerabilities during the CI/CD pipeline, alerting the team to any risks associated with outdated or insecure components. This proactive approach not only helps in mitigating security issues before they reach production but also supports compliance with industry standards by ensuring that container images are secure from the outset.

Once the applications are live, Defender for Containers continues to provide runtime protection. If an anomalous behavior is detected—such as unauthorized access attempts or unusual network traffic—the solution can automatically trigger alerts and initiate remediation steps. Additionally, it offers detailed insights into security posture and potential attack paths within the container environment. This holistic security approach allows organizations to focus on innovation and agility while maintaining a strong security foundation, ultimately enabling them to deliver secure applications to their customers confidently.

## Lab Objectives

You will be able to complete the following tasks:

- Task 1: Verify Docker Installation
- Task 2: Download vulnerable image from Docker Hub into the Container Registry
- Task 3: Investigate the recommendation for vulnerabilities in ACR

## Task 1: Verify Docker Installation

1. From the **Virtual Machine** desktop click on **Docker**.
 
    ![](images/m2-img1.png)

2. Click **Accept** on **Docker Subscription Service Agreement**.

    ![](images/m2-img2.png)

3. Next, Click on **Skip**.

    ![](images/m2-img3.png)

4. Wait for the **Docker Engine** to start. 

    ![](images/m2-img4.png)
    
5. Search for PowerShell in Search bar and select **Windows PowerShell**.

   ![Open Powershell](images/open-powershell.png)

6. Verify your docker version by executing in PowerShell. 

   ```
   docker version
   ```

   You may see an output like the one below:

   ![Docker Version in Powershell](images/docker-version.png)


## Task 2: Download vulnerable image from Docker Hub into the Container Registry

Now you will use Docker to download a vulnerable image from it and push it into our existing Azure Container registry.

1. Navigate to the Azure Portal, search for **container** **(1)** in the search box and select **Container registries** **(2)**.

   ![Container registry in Azure](images/serach-cr.png)

2. Open the Container Registry named **asclabcrxxxxxx**.

   ![Container registry open](images/select-cr.png)

3. In the Overview of it, verify the Login server name only. 

   ![ACR server name](images/copy-crname.png)

4.	Switch back to PowerShell, you will also need to login to your Azure subscription via **az login**. Enter the following **Email/Username** and **Password** in the browser and click on **Sign in**:

      * Email/Username: **<inject key="AzureAdUserEmail" enableCopy="true"/>** 

      * Password: **<inject key="AzureAdUserPassword" enableCopy="true"/>**

5. Make sure to update **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command.
   
   ```
   az acr login --name NameOfServer
   ```
 
   ![ACR login](images/acr-login.png)

6. Download vulnerable image from docker hub, by running the command below in PowerShell:

   ```
   docker pull vulnerables/web-dvwa
   ```

   ![ACR login](images/docker-pull1.png)

7. Check the image on your local repository by running the command below:

   ```
   docker images vulnerables/web-dvwa
   ```

   ![Docker images](images/docker-pull2.png)

8. Create an alias of the image by running the following command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

   ```
   docker tag vulnerables/web-dvwa NameOfServer.azurecr.io/vulnerables/web-dvwa
   ```

9. Check again the image on your local repository by running the command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

   ```
   docker images NameOfServer.azurecr.io/vulnerables/web-dvwa
   ```

   ![Docker images](images/docker-image.png)


10. Run docker push to upload the new image to the azure repository and generate image scan (it can take some time), using the below command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

    ```
    docker push NameOfServer.azurecr.io/vulnerables/web-dvwa
    ```

    ![Docker images](images/docker-push.png)

11. Then navigate back to the Azure portal and open the Container registry named **<inject key="Container registry" enableCopy="true"/>**.

12. Now select **Repositories** **(1)** under Services in the **<inject key="Container registry" enableCopy="false"/>** Container Registry resource. Notice the **vulnerable image** **(2)** is found in the ACR repository.

    ![Image in ACR](images/cr-repos.png)

## Task 3: Investigate the recommendation for vulnerabilities in ACR

Once a vulnerable image has been pushed to the Azure Container Registry, then Microsoft Defender for Containers will start scanning the image for vulnerabilities, by using Qualys. You will now look into the recommendation in Microsoft Defender for Cloud for this. 
 
1. In the Azure Portal, search for Microsoft Defender **(1)** in the search box and then select **Microsoft Defender for Cloud** **(2)**.

    ![Microsoft Defender](images/m2-ex3-step1.png)
   
2. From the **Microsoft Defender for Cloud** pane, select **Recommendations** from left-menu under General.

    ![Microsoft Defender](images/m2-ex3-step2.png)
 
3. Now under Secure score recommendations pane, set the **Resource type** filter to have it equal to **Container registries** **(1)** and then expand the **Remediate vulnerabilities** **(2)**. Click on the recommendation **Container registry images should have vulnerability findings resolved** **(3)** to get more details about it.  
   ![Recommendation for vulnerabilities in ACR](images/m2-ex3-step3.1.png)

4. Look around at what's available in the recommendation. Take a note of the Remediation Steps.

   ![Remediation Steps](images/m2-ex3-step4.png)
  
5. Select the vulnerability **Container registry images should have vulnerability findings resolved**, under **Security Checks**, select one of the items in the list to get additional details about the patch available for it and how to remediate it.

   ![Debian](images/m2-ex3-step5.png)
 
## Summary

In this exercise, you verified the installation of Docker to ensure the environment was properly set up for container management. Next, you downloaded a vulnerable image from Docker Hub into the Azure Container Registry (ACR) to simulate potential security risks. Finally, you investigated the recommendations provided by Defender for Containers regarding vulnerabilities in the ACR, allowing you to understand how to mitigate these risks and enhance the security of your containerized applications.

### You have successfully completed the lab
