# AWS S3 Bucket + Bucket Policy (Fix AccessDenied)

This project shows how I created an **Amazon S3 bucket**, uploaded an object, then fixed the **`AccessDenied`** error when opening the S3 **Object URL** by configuring **S3 permissions + a Bucket Policy**.

> Region used: **Asia Pacific (Singapore) — `ap-southeast-1`**  
> Demo bucket: **`ashraf-s3-demo-bucket-2026`**

---

## What are the content
- Create an S3 bucket (AWS Console)
- Upload an object
- Understand why **Object URL** returns `AccessDenied`
- Fix public access using:
  - **Block Public Access settings**
  - **Bucket Policy (s3:GetObject)**
- Verify public access by loading the Object URL in browser

---

## 🏗️ System Architecture

<p align="center">
  <img src=docs/images/aws-s3-bucket-policy.png" width="800" />
</p>

This diagram illustrates the flow on how to host s3 object in aws.

## Screenshots (Step-by-step)

### Step 1 — Open S3 in AWS Console
<p align="center">
  <img src="docs/images/Project 1 - Step 1.png" width="500" />

### Step 2 — View buckets list

<p align="center">
  <img src="docs/images/Project 1 - Step 2.png" width="500" />
</p>

### Step 3 — Create bucket (Singapore region)

<p align="center">
  <img src="docs/images/Project 1 - Step 3.png" width="500" />
</p>

### Step 4 — Keep Block Public Access OFF
This is AWS default and recommended.

<p align="center">
  <img src="docs/images/Project 1 - Step 4.png" width="500" />
</p>

### Step 5 — Bucket created

<p align="center">
  <img src="docs/images/Project 1 - Step 5.png" width="500" />
</p>

### Step 6 — Bucket is empty

<p align="center">
  <img src="docs/images/Project 1 - Step 6.png" width="500" />
</p>

### Step 7 — Upload a file

<p align="center">
  <img src="docs/images/Project 1 - Step 7.png" width="500" />
</p>

### Step 8 — Upload success

<p align="center">
  <img src="docs/images/Project 1 - Step 8.png" width="500" />
</p>

### Step 9 — Copy Object URL (test access)

<p align="center">
  <img src="docs/images/Project 1 - Step 9.png" width="500" />
</p>

### Step 10 — Problem: Object URL shows `AccessDenied`
Because the object is private by default.

<p align="center">
  <img src="docs/images/Project 1 - Step 10.png" width="800" />
</p>

---

## Why `AccessDenied` happens
By default:
- S3 objects are **private**
- Bucket has **no policy** allowing public reads
- **Block Public Access** prevents public policies from working (if enabled)

So opening the Object URL returns:
- `Code: AccessDenied`
- `Message: Access Denied`

---

## Fix AccessDenied (Permissions + Bucket Policy)

### Step 11 — Go to Bucket → Permissions
Open:
**S3 → Your bucket → Permissions tab**

<p align="center">
  <img src="docs/images/Project 1 - Step 11.png" width="500" />
</p>

Open:
**Permissions → Block public access (bucket settings) → Edit**

> ⚠️ Security note: Public access is only for learning/demo or public assets.

### Step 12 — Add a Bucket Policy (Public Read)
Open:
**Permissions → Bucket policy → Edit**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadSingleObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::ashraf-s3-demo-bucket-2026/honda-civic-type-r-3840x2160-20886.jpg"
    }
  ]
}
```

<p align="center">
  <img src="docs/images/Project 1 - Step 12.png" width="500" />
</p>

### Step 13 — Now can access the S3 Object URL

<p align="center">
  <img src="docs/images/Project 1 - Step 14.png" width="500" />
</p>
