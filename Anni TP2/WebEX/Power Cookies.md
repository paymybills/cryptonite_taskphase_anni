# PicoCTF Challenge: Power Cookie

### Challenge Description:
In this challenge, we need to manipulate cookies to gain access and capture the flag.

---

### Steps to Solve:

1. **Launch the Instance:**
   - Start by visiting the PicoCTF website and find the challenge called "Power Cookie".
   - Click on "Launch instance" to start the challenge. Note that you have a 15-minute timer to solve it.

2. **Access the Website:**
   - Click on "Go to this website and see what you can discover."
   - Once the website opens, click on "continue as guest."

3. **Inspect the Cookies:**
   - Since the challenge is related to cookies, open the browser's developer tools (usually by pressing `F12` or `Ctrl+Shift+I`).
   - Go to the "Network" tab and reload the page.
   - Look for a request with a status of 200 and click on it.
   - Move to the "Cookies" tab and find a cookie named `admin` with a value of `0`.

4. **Modify the Cookie:**
   - Go to the "Storage" tab, find the `admin` cookie, and change its value from `0` to `1`.
   - Refresh the page.

5. **Capture the Flag:**
   - After refreshing the page, you should see the flag.

---

### Flag:
`picoCTF{gr4d3_A_c00k13_5d2505be}`

---
