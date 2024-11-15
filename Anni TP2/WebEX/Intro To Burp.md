# PicoCTF Challenge: IntroToBurp

**Challenge Description**:  
In this challenge, the goal is to use Burp Suite to intercept and manipulate web traffic in order to bypass a 2FA (two-factor authentication) mechanism and capture the flag.

---

## Steps to Solve:

### 1. **Launch the Instance:**
   - Start by launching the instance provided by PicoCTF.
   - The page will present with a registration form where you'll need to input some data.

### 2. **Intercept the Registration Request:**
   - Fill in the registration form with some arbitrary data.
   - Click the **"Register"** button.
   - Open **Burp Suite** and use the proxy feature to intercept the HTTP request that is sent to the server.

### 3. **Modify the Request:**
   - In **Burp Suite**, locate the intercepted request within the "Intercept" tab.
   - Look for the parameter `otp=123` in the raw request data.
   - Delete the line containing `otp=123`.

### 4. **Forward the Modified Request:**
   - After modifying the request by removing the `otp=123` parameter, click **"Forward"** in Burp Suite.
   - This forwards the altered request to the server.

### 5. **Capture the Flag:**
   - Since the 2FA mechanism has been bypassed by removing the `otp=123` parameter, the server will respond as if the authentication was successful.
   - The response from the server will contain the flag, completing the challenge.

---

### Flag:

Once you bypass the 2FA, the flag will be returned in the server’s response.
Flag:
picoCTF{#0TP_Bypvss_SuCc3$$_b3fa4f1a}


---
