# JASS Ransomware Decryptor

Credits to [**Rivitna**](https://x.com/rivitna2) for providing the base Python Decryptor Script. This is a port to C# which adds a graphical interface, automated decryption eliminating manual single file decryption, report summary and log generation.

## Recovery behavior

### Keep encrypted files enabled

**Keep encrypted files (recommended)** is enabled by default, recovered files are written beside their encrypted counterparts and the `.jass` originals are retained.

![Keep Encrypted Files Enabled](https://media.githubusercontent.com/media/Xyntrax/JASS-Decryptor/main/images/K-E-F-E.gif)

### Keep encrypted files disabled

When the option is unchecked, it attempts to delete the matching encrypted `.jass` source only after its recovered output has been written successfully.

![Keep Encrypted Files Disabled](https://media.githubusercontent.com/media/Xyntrax/JASS-Decryptor/main/images/K-E-F-D.gif)

## How the recovery works

The port follows the supplied recovery routine: it XORs the first 20,000 bytes of each candidate file with the corresponding bytes of the embedded key stream. Bytes after that prefix are left unchanged. The transformation has no independent authentication tag or built-in content-integrity check.

For a known encrypted/original pair, compare the recovered file with the original, for example by comparing SHA-256 hashes. A match validates that sample, not every file or every ransomware infection.

## Features

- Discovers fixed and removable drives; `C:` is selected by default.
- Optional scanning of mapped network drives.
- Supports selecting individual folders and files in addition to drive selections.
- Recursively searches selected directories for files ending in `.jass`.
- Writes recovered outputs beside the encrypted source, removing the final `.jass` extension. For example, `document.doc.jass` becomes `document.doc`.
- Does not overwrite an existing output; an existing destination is reported as skipped.
- Shows a summary result and saves a timestamped recovery report.
