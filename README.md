# Social Studio Releases

This repository hosts official, cryptographically signed release packages and installation tooling for Social Studio.

Social Studio is a self-hosted social media planning, composer, and publishing platform designed to run on standard web hosting accounts.

---

## What Is in This Repository

This repository contains release distribution artifacts for customer installations:

- **`manifest.json`**: Release manifest detailing the latest version, release timestamp, minimum requirements, and package SHA-256 checksum.
- **`manifest.sig`**: Detached Ed25519 digital cryptographic signature for `manifest.json`.
- **`socialstudio-X.Y.Z.zip`**: Complete application archive containing verified runtime code and web assets.
- **`install.php`**: One-file web installer wizard for deploying Social Studio to cPanel or compatible hosting.

---

## How to Install Social Studio

To deploy a clean installation on your hosting account:

1. Download the latest `install.php` from the [Latest Release](https://github.com/konguspng/socialstudio-releases/releases/latest) section.
2. Upload `install.php` to your website document root (such as `public_html` or a subdomain folder) using cPanel File Manager or FTP.
3. Open the installer link in your web browser:  
   `https://yourdomain.com/install.php?k=YOUR_KEY`  
   (If you generated the installer locally, use the secret access key displayed during build).
4. Follow the on-screen wizard to verify server compatibility, enter your company name, create your administrator account, and configure the background scheduler.
5. Click **Remove Installer** once finished to delete `install.php` from your server.

---

## How Updates Are Verified

Social Studio features an automated background updater designed for reliability and zero downtime:

1. **Cryptographic Signatures**: Every release manifest is signed with an Ed25519 private key. Installed copies verify this signature against their built-in public key before downloading or unpacking code.
2. **Checksum Integrity**: Application archives are verified against the manifest SHA-256 hash.
3. **Isolated Pre-Activation Smoke Test**: New versions are extracted into an isolated staging directory (`studio-app.new`) where an automated syntax and import test verifies runtime health before activating.
4. **Atomic Swapping and Rollback**: The active directory is swapped atomically. If an update encounters an issue during staging, the previous stable version in `studio-app.prev` remains active and the update rolls back automatically.
5. **Data Protection**: Your database, uploaded media, connection secrets, and configuration live in `studio-data/` and are never overwritten or deleted by updates.

---

## Reporting Issues

If you encounter an issue or have questions about installation, please reach out to your studio provider or file an issue in this repository.
