

# **Amazon RDS Multi-AZ and Read Replica Deployment**

## **Introduction**
This project demonstrates how to work with Amazon RDS (Relational Database Service) to:
- Enable **Multi-AZ deployment** for high availability and failover.
- Create and promote a **Read Replica** to enhance performance and support disaster recovery.
- Update the database endpoint in **Route 53** to reflect the promoted instance.

The hands-on lab provides a step-by-step guide to configuring RDS for failover and read scalability.

---

## **Objectives**
1. Enable **Multi-AZ Deployment** to ensure database availability in case of failures.
2. Create and configure **Read Replicas** for better performance and scalability.
3. Simulate failovers and test **DNS-based endpoint redirection** using **Route 53**.

---

## **Prerequisites**
- AWS account with access to the **N. Virginia (us-east-1)** region.
- Existing WordPress database in Amazon RDS.
- Basic understanding of AWS services (EC2, RDS, and Route 53).

---

## **Steps to Deploy**

### **1. Enable Multi-AZ Deployment**
1. Navigate to **RDS** in the AWS Management Console.
2. Select your WordPress database instance and click **Modify**.
3. Under **Availability & durability**, enable **Create a standby instance (recommended for production usage)**.
4. Scroll down and click **Continue**, then choose **Apply immediately**.
5. Wait for the status to update to **Modifying** (may take up to 10 minutes).
6. Verify Multi-AZ deployment:
   - Navigate to the **Events** section in the RDS sidebar.
   - Check for an event indicating the instance has been converted to Multi-AZ.

### **2. Test Multi-AZ Failover**
1. Reboot the instance with failover:
   - Go to **Databases** in the RDS sidebar, select your instance, and choose **Reboot with Failover** from the **Actions** dropdown.
2. Observe the failover:
   - The standby instance will take over as the primary.
   - Refresh your DNS web page to confirm minimal downtime.

---

### **3. Create a Read Replica**
1. In the **RDS** console, select your WordPress instance and choose **Create read replica** from the **Actions** dropdown.
2. Configure the replica:
   - Set the instance identifier to `wordpress-rr`.
   - Ensure the **Destination Region** is set to **US East (N. Virginia)**.
   - Leave other settings as default and click **Create read replica**.
3. Wait for the read replica to become available (5-10 minutes).
4. Verify that the DNS web page remains operational during this process.

---

### **4. Promote the Read Replica**
1. Select the read replica in the RDS console and choose **Promote** from the **Actions** dropdown.
2. Leave all defaults and click **Promote read replica**.
3. Wait for the status to change from **Replica** to **Instance** and ensure it is available.

---

### **5. Update the Route 53 CNAME Record**
1. Copy the new read replica endpoint:
   - Select the promoted instance and copy the **Endpoint** from the **Connectivity & security** tab.
2. Update the CNAME record:
   - Navigate to **Route 53** and select your hosted zone (e.g., `mydomain.local`).
   - Edit the CNAME record pointing to your WordPress database and replace it with the new endpoint.
   - Save the changes.
3. Verify no downtime:
   - Refresh your DNS web page to confirm uninterrupted service.

---

## **Key Features**
- **Multi-AZ Deployment**: Provides high availability by automatically failing over to a standby instance in another availability zone.
- **Read Replicas**: Improves performance by distributing read traffic and allows for seamless promotion in disaster recovery scenarios.
- **Route 53 Integration**: Ensures seamless endpoint redirection during database promotions with no downtime.

---

## **AWS Services Used**
- **Amazon RDS**:
  - Multi-AZ Deployment
  - Read Replicas
- **Amazon Route 53**:
  - DNS Management
  - CNAME Record Updates
- **Amazon EC2**:
  - For Load Balancing and DNS Testing

---

## **Expected Outcome**
- A highly available and scalable RDS setup with Multi-AZ enabled.
- Seamless transition from primary to standby instance during failover.
- Improved performance with read replicas and zero-downtime migrations using Route 53.

---


## **Conclusion**
This hands-on lab showcases how to deploy a resilient and scalable database solution using Amazon RDS. By combining Multi-AZ deployment, read replicas, and Route 53, you can ensure high availability, enhanced performance, and seamless disaster recovery.


