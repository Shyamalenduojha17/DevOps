
### 🔹 **Basic Level**

1. **What is Terraform and how is it different from other IaC tools like CloudFormation or Ansible?**  
   **Terraform** is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It allows you to define, provision, and manage infrastructure using a declarative configuration language.  
   - **CloudFormation** is AWS-specific, while Terraform is **cloud-agnostic**.  
   - **Ansible** is procedural and better suited for **configuration management**, whereas Terraform is **declarative** and focuses on **infrastructure provisioning**.

2. **What is the purpose of the `terraform init` command?**  
   It initializes a Terraform working directory by downloading the necessary **provider plugins**, initializing the backend, and preparing the directory for use.

3. **What are Terraform providers? Give some examples.**  
   Providers are plugins that interact with APIs of cloud platforms or services. They are the **bridge between Terraform and the platform** you're managing.  
   **Examples:**  
   - `aws` (Amazon Web Services)  
   - `azurerm` (Microsoft Azure)  
   - `google` (Google Cloud Platform)  
   - `kubernetes`, `docker`, `vault`

4. **What is the difference between `terraform plan` and `terraform apply`?**  
   - `terraform plan` shows a **preview** of what Terraform will do.  
   - `terraform apply` actually **executes** the changes required to reach the desired state.

5. **What is the use of a Terraform state file?**  
   The `.tfstate` file stores the **current state** of the infrastructure as known by Terraform. It allows Terraform to **track resources**, perform **diffs**, and determine what changes are needed.

6. **What is the difference between `terraform destroy` and `terraform taint`?**  
   - `terraform destroy` removes **all resources** managed by Terraform.  
   - `terraform taint` marks a **specific resource** for recreation on the next `apply`.

7. **What are modules in Terraform? Why are they useful?**  
   Modules are reusable groups of Terraform resources.  
   They're useful for:  
   - **Code reuse**  
   - **Consistency across environments**  
   - **Better organization and scalability**

8. **How does Terraform handle resource dependencies?**  
   Terraform uses **dependency graphs** (based on `depends_on` and resource references) to determine the **order of operations** during apply and destroy phases.

9. **What are input and output variables in Terraform?**  
   - **Input variables** are parameters passed into modules to customize behavior.  
   - **Output variables** are values returned from modules, which can be used in other modules or displayed post-deployment.

10. **What is the purpose of backend configuration in Terraform?**  
    The backend determines **where the state file is stored** (e.g., local, S3, Terraform Cloud).  
    It also handles **locking**, **remote operations**, and **collaboration support** for teams.

---

### 🔹 **Scenario-Based / Intermediate to Advanced**

11. **You accidentally deleted resources from the cloud console that are managed by Terraform. How do you reconcile this with Terraform?**  
    Run `terraform apply`. Terraform will detect the missing resource and **recreate it**. Alternatively, run `terraform plan` to review the impact first.

12. **You have a team collaborating on Terraform code. How do you manage the `.tfstate` file securely and avoid conflicts?**  
    - Use a **remote backend** (e.g., S3 with DynamoDB for locking).  
    - Enable **state locking** to prevent concurrent changes.  
    - Use **Terraform Cloud** or **workspaces** for team collaboration.

13. **You made manual changes in AWS that Terraform doesn’t know about. How do you sync Terraform’s state with the actual infrastructure?**  
    - Run `terraform refresh` to update the state file.  
    - If needed, use `terraform import` to bring unmanaged resources under Terraform control.

14. **You need to deploy the same infrastructure to dev, staging, and production environments. How do you structure your Terraform code?**  
    - Use a **modular structure** with separate `dev`, `staging`, and `prod` directories.  
    - Share modules and use **separate variable files and backends** per environment.

15. **You want to reuse infrastructure code with different configurations for each environment. How would you use modules and workspaces for this?**  
    - Create **generic modules** and call them with different inputs.  
    - Use **Terraform workspaces** to switch between environments dynamically.  
    - Combine modules with environment-specific **`terraform.tfvars`**.

16. **You're running a `terraform apply` and someone else on the team has changed the state in the meantime. What happens, and how do you prevent issues?**  
    Terraform will detect a **state lock** (if using remote backend with locking) and **fail gracefully**.  
    To prevent this:  
    - Use **state locking** (e.g., DynamoDB for S3 backend).  
    - Collaborate through **Terraform Cloud** or **version control practices**.

17. **You want to manage secrets in your Terraform code (like database passwords). What are some best practices?**  
    - Use **environment variables** or **encrypted variable files**.  
    - Use **secrets managers** (e.g., AWS Secrets Manager, Vault) and pull secrets dynamically.  
    - Avoid hardcoding secrets or committing them to version control.

18. **You're using Terraform in a CI/CD pipeline and the build fails due to a locking error on the state file. How do you resolve this?**  
    - Ensure **state locking is enabled** (e.g., DynamoDB for S3 backend).  
    - Use `terraform force-unlock` with caution if a lock is stuck.  
    - Consider adding retry logic or timeout settings in CI/CD.

19. **How would you roll back to a previous known-good state if a Terraform deployment introduces a breaking change in production?**  
    - Use **versioned state files** (e.g., in S3) to restore a backup.  
    - Revert the code changes and re-apply.  
    - Keep a **backup of state files** and use `terraform state push` if needed.

20. **How would you handle deploying resources in multiple AWS regions using Terraform?**  
    - Use **provider aliasing** to define multiple regions:  
      ```hcl
      provider "aws" {
        alias  = "us_east"
        region = "us-east-1"
      }

      provider "aws" {
        alias  = "us_west"
        region = "us-west-2"
      }
      ```  
    - Then assign resources to appropriate provider using `provider = aws.us_west`, etc.

21. **You are using Terraform in a CI/CD pipeline, and the build fails due to a **locking error** on the state file. How do you resolve this issue?**

✅ **Answer:**

When Terraform encounters a **locking error** on the state file in a CI/CD pipeline, it means that another Terraform operation is currently modifying the state, and the current operation is being blocked to prevent state corruption.

Here’s how you can resolve it:

1. **Ensure Proper Locking**:  
   - Terraform’s remote backends (like **S3 + DynamoDB** or **Terraform Cloud**) support state locking. Ensure **state locking** is enabled, which prevents multiple Terraform processes from modifying the state at the same time.

2. **Manual Unlock**:  
   - If you're sure no other processes are using the state, you can manually **unlock** the state file using the following command:
     ```bash
     terraform force-unlock LOCK_ID
     ```
     - **LOCK_ID** is the ID that Terraform provides when it encounters a lock. You can find it in the error message.

3. **Verify Running Processes**:  
   - Make sure no other Terraform processes are running. You can check for Terraform processes using:
     ```bash
     ps aux | grep terraform
     ```
   - If a process is running, it could be applying or planning changes, which can cause the locking issue.

4. **Pipeline Configuration**:
   - **Ensure proper concurrency** settings in the CI/CD pipeline to prevent multiple Terraform commands (apply, plan) from running simultaneously.
   - Use **lock file** or a similar mechanism to prevent concurrency issues in the pipeline.

5. **State File in Remote Backend**:  
   - If you're using a remote backend like **S3** with **DynamoDB** for state locking, ensure that your DynamoDB table is configured to handle concurrency correctly (i.e., it’s set up with proper **consistency**).

6. **Terraform Cloud/Enterprise**:
   - If you're using **Terraform Cloud** or **Enterprise**, it automatically manages locking for you, but if it fails, retrying the pipeline might resolve transient issues.


---
