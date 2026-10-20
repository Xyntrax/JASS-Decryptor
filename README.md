# JASS Ransomware Decryptor

Credits to [**Rivitna**](https://x.com/rivitna2) for providing the base Python Decryptor Script. This is a port to C# which adds a graphical interface, automated decryption eliminating manual single file decryption, report summary and log generation.

### Reference Case

This decryptor was developed for a specific ransomware case discussed on the Kaldata forums.

- https://www.kaldata.com/forums/topic/346429-системата-е-инфектирана-с-някакъв-ransomware/
- https://www.bleepingcomputer.com/forums/t/819569/unknown-ransomware-with-jass-extension-jass-decryptor-available/

*Note: `JASS` refers to the encrypted file extension appended by the ransomware sample. Its family has not been conclusively identified as the sample appears to have self-deleted, but it was a homemade ransomware.*

## Recovery Behavior

### Keep Encrypted Files Enabled

**Keep Encrypted Files (recommended)** is enabled by default, recovered files are written beside their encrypted counterparts and the `.jass` originals are retained.

![Keep Encrypted Files Enabled](https://media.githubusercontent.com/media/Xyntrax/JASS-Decryptor/main/images/K-E-F-E.gif)

### Keep Encrypted Files Disabled

When the option is unchecked, it attempts to delete the matching encrypted `.jass` source only after its recovered output has been written successfully.

![Keep Encrypted Files Disabled](https://media.githubusercontent.com/media/Xyntrax/JASS-Decryptor/main/images/K-E-F-D.gif)

## How Decryption Works

The decryptor uses an embedded key stream to reverse the XOR transformation applied to the first 20,000 bytes of each encrypted file. The rest of the file is left unchanged.

To verify a recovered file, you can compare its SHA-256 hash with that of a known good original copy. Matching hashes confirm that both files have identical contents.

## Features

- Discovers fixed and removable drives; `C:` is selected by default.
- Optional scanning of mapped network drives.
- Supports selecting individual folders and files in addition to drive selections.
- Recursively searches selected directories for files ending in `.jass`.
- Writes recovered outputs beside the encrypted source, removing the final `.jass` extension. For example, `document.doc.jass` becomes `document.doc`.
- Does not overwrite an existing output; an existing destination is reported as skipped.
- Shows a summary result and saves a timestamped recovery report.
