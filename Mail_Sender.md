Let's go step by step to **fix your PHPMailer issue**.

---

# **🔹 Step 1: Identify the Error**
Your **original error** was:
```
Message could not be sent. Mailer Error: Invalid address:  (From):
```
This means **PHPMailer is not getting a valid sender email address**.

---

# **🔹 Step 2: Fix Your PHPMailer Code**
### **1️⃣ Ensure You Are Using Correct Code**
Your current `sendmail.php` file has some issues, so use this **corrected version**:

```php
<?php 
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;

require 'vendor/autoload.php';

// Load configuration
$config = require 'config.php';

$mail = new PHPMailer(true);

try {
    // Enable Debugging for More Details
    $mail->SMTPDebug = 2;  
    $mail->Debugoutput = 'html';

    // Server settings
    $mail->isSMTP();
    $mail->Host       = $config['smtp_host'];  
    $mail->SMTPAuth   = true;
    $mail->Username   = $config['email'];    
    $mail->Password   = $config['password'];  
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
    $mail->Port       = $config['smtp_port'];

    // Set From Email Address (Fix Invalid Address Error)
    $mail->setFrom($config['email'], 'Rajnesh Rai');

    // Set Recipient Email Address
    $mail->addAddress('rajneeshrai1204@gmail.com'); 

    // Email Content
    $mail->isHTML(true);
    $mail->Subject = 'Test Email from PHPMailer';
    $mail->Body    = 'This is a test email!';

    $mail->send();
    echo '✅ Email has been sent!';
} catch (Exception $e) {
    echo "❌ Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
```

### ✅ **What We Fixed?**
- **Properly set the `setFrom()` email address** using `config.php`.
- **Added debugging (`SMTPDebug = 2`)** to get better error messages.
- **Removed duplicate configuration code** at the bottom.

---

# **🔹 Step 3: Check `config.php`**
Make sure **`config.php`** has valid SMTP settings.

### ✅ **Correct `config.php`**
```php
<?php
return [
    'email' => 'your-email@gmail.com',  // Use your Gmail address
    'password' => 'your-app-password',  // Use a Gmail App Password (NOT your Gmail password)
    'smtp_host' => 'smtp.gmail.com',
    'smtp_port' => 587
];
```
🔹 **Replace `your-email@gmail.com`** with your actual email.  
🔹 **Replace `your-app-password`** with a **Gmail App Password** (explained in Step 7 below).  

---

# **🔹 Step 4: Verify Composer Installation**
To use PHPMailer, you must install it using **Composer**.

### ✅ **Check if Composer is Installed**
Run this command in PowerShell:
```powershell
composer -v
```
🔹 If you see Composer’s version, it’s installed.  
🔹 If **not found**, install it from: [https://getcomposer.org/download/](https://getcomposer.org/download/)

---

# **🔹 Step 5: Install PHPMailer**
Once Composer is installed, install PHPMailer by running:
```powershell
composer require phpmailer/phpmailer
```
🔹 This will download and install PHPMailer in your project.

---

# **🔹 Step 6: Ensure PHP is Installed Correctly**
PHPMailer needs PHP installed.

### ✅ **Check if PHP is Installed**
Run:
```powershell
php -v
```
🔹 If PHP is **not recognized**, you need to **add it to your system’s PATH**.

---

# **🔹 Step 7: Enable Gmail SMTP (Important!)**
By default, **Google blocks PHPMailer** unless you do these steps:

### ✅ **1️⃣ Enable 2-Step Verification in Gmail**
1. Open **Google Security Settings**:  
   🔗 [https://myaccount.google.com/security](https://myaccount.google.com/security)
2. Find **"2-Step Verification"** and **enable it**.

---

### ✅ **2️⃣ Generate an App Password**
1. Go to **Google App Passwords**:  
   🔗 [https://myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)
2. **Choose "Mail"** and select your device (or choose "Other" and type "PHPMailer").
3. Google will generate a **16-character password**.
4. Copy this password and use it in **`config.php`** instead of your actual Gmail password.

---

### ✅ **3️⃣ Allow Less Secure Apps (If Needed)**
1. Go to:  
   🔗 [https://myaccount.google.com/lesssecureapps](https://myaccount.google.com/lesssecureapps)
2. Enable **"Less Secure Apps"**.

---

# **🔹 Step 8: Test Email Sending Again**
Now, go to **PowerShell** and run:
```powershell
php sendmail.php
```
🔹 If everything is correct, you should see:
```
✅ Email has been sent!
```
🔹 If there is still an error, check the **debug output** for details.

---

# **✅ Final Checklist**
✅ `sendmail.php` is **correct**.  
✅ `config.php` has **valid email and app password**.  
✅ **Composer is installed** (`composer -v`).  
✅ **PHPMailer is installed** (`composer require phpmailer/phpmailer`).  
✅ **PHP is installed** (`php -v`).  
✅ **Gmail SMTP settings are configured** (App Password, 2-Step Verification).

---

Try these steps **one by one** and let me know where you face any issues! 🚀
