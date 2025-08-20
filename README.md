# Assignment 2: Secure File Hosting with S3 and IAM

## 🎯 Objective  
Practice with **Amazon S3 bucket policies** and **IAM user permissions** by securely hosting and testing file access with the AWS CLI.  

---

## 📌 Tasks
- Create an S3 bucket named: `<yourname>-assignment-bucket`.  
- Upload a sample file (e.g., resume or a dummy PDF).  
- Create an IAM user `s3-access-user` with **programmatic access**.  
- Attach a **custom policy** allowing only `list` and `get object` permissions on the bucket.  
- Test access using the AWS CLI with the IAM user's credentials.  

Deliverables:  
- ✅ Policy JSON  
- ✅ Screenshot showing successful `aws s3 ls` and `aws s3 cp` from the new user.  

---

## 🛠️ Steps Performed  

### Step 1: Create S3 Bucket  
1. Go to **AWS Management Console → S3**.  
2. Click **Create bucket**.  
3. Bucket name: `harshitprajapati-assignment-bucket`  
   Region: `ap-south-1`  
4. Block all public access (default).  
5. Click **Create bucket**.  

---

### Step 2: Upload a Sample File  
1. Open the bucket.  
2. Click **Upload → Add files**.  
3. Upload file: `Harshit Prajapati-ResumeLCD.pdf`.  
4. Confirm upload.  

---

### Step 3: Create IAM User  
1. Go to **IAM → Users → Create user**.  
2. User name: `s3-access-user`.  
3. Select **Programmatic access**.  
4. Save **Access Key ID** and **Secret Access Key** securely.  

---

### Step 4: Attach Custom Policy  

**Policy JSON**  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetBucketLocation"
      ],
      "Resource": "arn:aws:s3:::harshitprajapati-assignment-bucket"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::harshitprajapati-assignment-bucket/*"
    }
  ]
}
```
Attached this policy to the IAM user s3-access-user.

---
### Step 5: Test via AWS CLI
Configure IAM Credentials
```bash
aws configure
# Enter Access Key, Secret Key, Region (ap-south-1), Output format: json
```

List Bucket Contents
```bash
aws s3 ls s3://harshitprajapati-assignment-bucket
```

Download a File
```bash
aws s3 cp s3://harshitprajapati-assignment-bucket/Harshit\ Prajapati-\ ResumeLCD.pdf ./ResumeLCD.pdf
```

Upload a File (expected Access Denied since only Get/List allowed)
```bash
aws s3 cp ./test.txt s3://harshitprajapati-assignment-bucket/
```
