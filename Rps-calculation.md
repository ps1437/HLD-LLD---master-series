
# Image Update Handling (Maximum 5MB) for Scalable URL Shortener Service

## 1. **Overview**
In addition to shortening URLs, the service also handles image uploads with the restriction that the maximum image size should not exceed **5MB**. This section covers the **database space calculation**, **requests per second (RPS)**, and **server calculation** in the context of handling image uploads and updates.

---

## 2. **Image Storage Considerations**

### 2.1. **Assumptions**
- Maximum image size: **5MB** (5,120,000 bytes).
- The service stores both the image and a reference to its metadata (URL or file path).
- **Image Metadata** (e.g., image format, size) requires 500 bytes for each image.

#### **Formula for Database Space per Image:**
- **Space per image = Image size + Metadata**
- **Space per image = 5,120,000 bytes + 500 bytes = 5,120,500 bytes** (approximately **5MB per image**).

#### **Example:**
Let’s assume the system stores **100 million images**.

- Total space for storing **100 million images**:
  
  ```python
  total_images = 100_000_000  # 100 million images
  space_per_image = 5120500  # bytes
  total_image_space = total_images * space_per_image  # in bytes
  total_image_space_gb = total_image_space / (1024 ** 3)  # converting to GB
  total_image_space_gb
  ```

- Total space required:

  ```python
  total_image_space = 100_000_000 * 5120500  # Total space in bytes
  total_image_space_gb = total_image_space / (1024 ** 3)  # Convert bytes to GB
  total_image_space_gb = 477.13 GB
  ```

So, the **database space required** to store **100 million images** is approximately **477.13 GB**.

---

## 3. **Requests per Second (RPS) Calculation for Image Uploads**

### 3.1. **Assumptions**
- Assume **100 million users**.
- Each user generates an average of **1 image upload request per day**.
- Total requests per user per day = **1 image upload per day**.

#### **Formula for RPS for Image Uploads:**
- **Total image upload requests per day = Number of users × Requests per user per day**
- **RPS for Image Uploads = Total image upload requests per day ÷ 24 hours/day ÷ 60 minutes/hour ÷ 60 seconds/minute**

#### **Example:**
- Total image upload requests per day for **100 million users**:

  ```python
  total_image_upload_per_user_per_day = 1  # 1 image upload per user per day
  total_users = 100_000_000  # 100 million users
  total_image_uploads_per_day = total_users * total_image_upload_per_user_per_day  # in requests
  total_image_uploads_per_day
  ```

- Total image upload requests per day:

  ```python
  total_image_uploads_per_day = 100_000_000 * 1  # 100 million image uploads per day
  ```

- RPS (Requests per Second for image uploads):

  ```python
  seconds_per_day = 24 * 60 * 60  # Number of seconds in a day
  rps_image_upload = total_image_uploads_per_day / seconds_per_day  # Requests per second
  rps_image_upload
  ```

- Total RPS for image uploads:

  ```python
  rps_image_upload = 100_000_000 / (24 * 60 * 60)  # RPS for image uploads
  rps_image_upload = 1,157 RPS
  ```

So, the system needs to handle approximately **1,157 RPS** for image uploads.

---

## 4. **Server Calculation for Image Uploads**

### 4.1. **Assumptions**
- Each server can handle **1,000 RPS**.
- The system needs to handle **1,157 RPS** for image uploads.

#### **Formula for Server Calculation:**
- **Number of servers for image uploads = RPS for image uploads ÷ RPS per server**

#### **Example:**
Given that each server can handle **1,000 RPS**, the number of servers required to handle image uploads is:

```python
rps_per_server = 1000  # RPS per server
required_rps_image_upload = 1157  # RPS for image uploads
servers_required_image_upload = required_rps_image_upload / rps_per_server  # Number of servers
servers_required_image_upload
```

- Number of servers required for image uploads:

```python
servers_required_image_upload = 1157 / 1000  # 1.16 servers
servers_required_image_upload = 2  # Round up to the nearest whole number
```

Thus, the system would need **2 servers** to handle **1,157 RPS** for image uploads.

---

## 5. **Summary of Calculations**

### 5.1. **Database Space Required for Images:**
- To store **100 million images**, the total database space required is approximately **477.13 GB**.

### 5.2. **RPS Handling for Image Uploads:**
- The system needs to handle approximately **1,157 RPS** for image uploads.

### 5.3. **Server Requirements for Image Uploads:**
- To handle **1,157 RPS** for image uploads, approximately **2 servers** would be required (assuming each server can handle **1,000 RPS**).

---

## 6. **Conclusion**

By calculating the **database space**, **RPS**, and **server requirements** for image uploads, we can design a scalable URL shortener service that also efficiently handles image updates. The system must store large images and efficiently manage the requests with horizontal scaling and optimized database usage.
