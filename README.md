# README: Deploying a Static Website Using AWS EC2 and S3

Welcome to the quick guide on how to host a static website using AWS EC2 (Elastic Compute Cloud) and S3 (Simple Storage Service). 

## :rocket: Introduction

- S3 (Simple Storage Service) lets you store files in the cloud—and one of its lesser-known superpowers is that it can serve websites too! It’s perfect for static websites (those made with just HTML, CSS, and JavaScript), and if you're on the AWS Free Tier, you can host up to 5GB of content for free for a whole year.
- Amazon EC2 provides resizable virtual servers in the cloud, giving you full control over your web server environment. It's perfect for hosting dynamic websites, custom apps, or serving static content with greater flexibility.

## :scroll: Step-by-Step Guide

Follow these steps to host your static website Using AWS EC2 and S3:

1. **Log into AWS**
   
   - Go to your AWS console and search for "S3" in the search bar, then select "S3" when it appears.

2. **Create a Bucket**

   - Click on "Create bucket."
   - Give your bucket a unique name (think of it like a folder name on the internet).
   - Choose your preferred region.

3. **Adjust Bucket Permissions**

   - Scroll to the Block Public Access section and uncheck “Block all public access”.
   - AWS will warn you about making the bucket public—confirm that this is what you want.

4. **Select Your Bucket**

   - Once created, select your bucket from the list.

5. **Bucket Policy for File Access**

   - Create a bucket policy to enable access to the files.
   - Navigate to the "Permissions" tab and under the "Bucket policy" section, enter the provided policy, ensuring to change the Resource to your bucket's ARN followed by "/*".
    
    * **Note your bucket ARN**, and replace `your-bucket-name` below.

      **Bucket Policy:**
      
      ```json
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "PublicReadGetObject",
                  "Effect": "Allow",
                  "Principal": "*",
                  "Action": "s3:GetObject",
                  "Resource": "arn:aws:s3:::your-bucket-name/*"
              }
          ]
      }
      ```
      > 💡 You can also use the [AWS Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html) to create a custom policy.

6. **Launch EC2 Instance and Connect via SSH**

  * **Launch EC2 Instance:** Use AWS Management Console to create a new EC2 instance.
  * **Connect to EC2:**

```bash
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-dns
```

---

7. **Install Web Server on EC2**

```bash
sudo yum update -y

sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd

sudo usermod -a -G apache ec2-user
sudo chmod 755 /var/www/html

cd /var/www/html
sudo touch index.html
sudo nano index.html

sudo touch style.css
sudo nano style.css
```

---
8. **update index.html and style.css**
* You can refer to the sample files I’ve shared.

9. **Access Your Website via EC2 Public IP**
* Find your **EC2 Public DNS/IP**
* Open your browser and go to:

```
http://your-ec2-public-dns
```
---
## :tada: Conclusion

With these steps, you can host your static website using AWS S3 and EC2. S3 stores your files, and EC2 gives you more control over how your site runs. Enjoy fast, easy, and flexible website hosting!

