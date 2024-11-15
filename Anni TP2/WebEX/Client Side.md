### PicoCTF Challenge: Don't Use Client-Side

**Challenge Description:**
In this challenge, we need to break into a "super secure" portal by finding the password hidden in the client-side code.

**Steps to Solve:**

1. **Access the Portal:**
   - Start by visiting the provided link to the "super secure" portal.

2. **Inspect the Page Source:**
   - Since no other instructions are given, the first step is to inspect the page source. This can be done by right-clicking on the page and selecting "View Page Source" or by pressing Ctrl+U.

3. **Find the Password:**
   - While inspecting the page source, look for any clues or hidden elements. In this case, the password is hidden within the HTML code.
   - The flag is found in parts within the page source. By joining these parts together, we get the complete flag.

4. **Capture the Flag:**
   - The flag for this challenge is picoCTF{no_clients_plz_b706c5}.
