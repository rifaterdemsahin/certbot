# README: Certbot Proof of Concept

This repository provides a detailed proof of concept (PoC) for using **Certbot** to automate the process of obtaining, installing, and renewing SSL/TLS certificates for a website. By following this guide, you'll learn how to set up Certbot on an Ubuntu server with Nginx, configure your website to use HTTPS, and automate the certificate renewal process.

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Obtaining an SSL Certificate](#obtaining-an-ssl-certificate)
5. [Automating Certificate Renewal](#automating-certificate-renewal)
6. [Verification and Maintenance](#verification-and-maintenance)
7. [License](#license)

## Introduction

Certbot is an open-source tool designed to simplify the process of securing a website with SSL/TLS certificates issued by **Let's Encrypt**. This PoC demonstrates how to install Certbot, obtain a certificate for a domain, and configure automatic renewal, providing a hands-free approach to maintaining HTTPS on your server.

## Prerequisites

Before you begin, ensure you have the following:

- An Ubuntu server with Nginx installed (or another supported web server).
- Root or sudo access to the server.
- A registered domain name pointing to your server's IP address.
- Basic familiarity with the Linux command line.

## Installation

1. **Update your package list and install Certbot**:

   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Verify Certbot installation**:

   Run the following command to check if Certbot was installed correctly:

   ```bash
   certbot --version
   ```

## Obtaining an SSL Certificate

1. **Run Certbot with Nginx plugin**:

   Use Certbot to obtain a certificate and configure Nginx to use it:

   ```bash
   sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
   ```

   Replace `yourdomain.com` with your actual domain name.

2. **Follow the prompts**:

   Certbot will ask for your email address and agreement to the Let’s Encrypt terms of service. Follow the on-screen instructions to complete the setup.

## Automating Certificate Renewal

1. **Test automatic renewal**:

   Check if Certbot can renew certificates automatically:

   ```bash
   sudo certbot renew --dry-run
   ```

   If this command completes without errors, your system is set up for automatic renewal.

2. **Schedule automatic renewal with Cron**:

   Certbot should automatically configure a cron job, but you can manually add one to ensure certificates are renewed twice daily:

   ```bash
   sudo crontab -e
   ```

   Add this line to your crontab:

   ```bash
   0 */12 * * * /usr/bin/certbot renew --quiet
   ```

## Verification and Maintenance

- **Verify HTTPS is working**:

  After obtaining the certificate, visit your site using `https://` to ensure the SSL is active.

- **Check renewal logs**:

  Periodically check Certbot logs in `/var/log/letsencrypt/` to ensure there are no errors with the renewal process.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

By following this README, you should have a fully automated SSL/TLS certificate setup using Certbot, ensuring your website is secure with minimal manual intervention. For more information, visit the [Certbot website](https://certbot.eff.org/).
