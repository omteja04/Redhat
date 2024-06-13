<!--
  Author: omteja04
  Created on: 09-06-2024 06:18:25
  Description: Umask
-->

<!-- cSpell:disable -->

```bash
# Switch to user natasha
su - natasha

# Edit .bash_profile
vim .bash_profile
```

(Add the line `umask 277` at the end of the file in `vim`, then save and exit with `:wq!`)

```bash
# Apply the updated .bash_profile
source .bash_profile

# Create a new directory
mkdir test

# Verify the directory permissions
ls -ld test

# Create a new file
touch testfile

# Verify the file permissions
ls -l testfile
```

### Expected Results and Permissions

#### **umask 277**

- The `umask` value `277` determines the default file creation permissions by subtracting the `umask` value from the system's default permissions.
- For directories: The default is `777` (rwxrwxrwx).
  - `777 - 277 = 500` which means `r-x------`.
- For files: The default is `666` (rw-rw-rw-).
  - `666 - 277 = 400` which means `r--------`.

### Permissions Verification

1. **Permissions of `test` Directory:**

   ```bash
   ls -ld test
   ```

   - Output: `dr-x------ natasha natasha test`
   - Explanation: The directory has permissions `500` which translates to `r-x------`.

2. **Permissions of `test/testfile` File:**
   ```bash
   ls -l test/testfile
   ```
   - Output: `-r-------- natasha natasha testfile`
   - Explanation: The file has permissions `400` which translates to `r--------`.

By following these steps, you'll ensure that the default permissions for newly created files and directories are set according to the `umask` value specified in the `.bash_profile`.
