<!--
  Author: omteja04
  Created on: 09-06-2024 06:07:57
  Description: Tar
-->

<!-- cSpell:disable
 -->

#### **1. Creating a gzipped tar archive**

```bash
tar -zcvf /root/test.tar.gz /var/tmp
```

- **`tar`**: The main command to create an archive.
- **`-z`**: Use gzip to compress the archive.
- **`-c`**: Create a new archive.
- **`-v`**: Verbosely list files processed.
- **`-f /root/test.tar.gz`**: Specify the name of the archive file to create.
- **`/var/tmp`**: The directory to include in the archive.

#### **2. Creating a bzip2-compressed tar archive**

```bash
tar -jcvf /root/test.tar.bz2 /var/tmp
```

- **`tar`**: The main command to create an archive.
- **`-j`**: Use bzip2 to compress the archive.
- **`-c`**: Create a new archive.
- **`-v`**: Verbosely list files processed.
- **`-f /root/test.tar.bz2`**: Specify the name of the archive file to create.
- **`/var/tmp`**: The directory to include in the archive.

### Comparison between gzip and bzip2

- **gzip** (`-z`):

  - Generally faster compression and decompression.
  - Produces larger files compared to bzip2.

- **bzip2** (`-j`):
  - Slower compression and decompression.
  - Produces smaller files compared to gzip.
