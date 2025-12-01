# Pollen Forecast Email Alert

![Pollen Alert](https://img.shields.io/badge/Pollen-Alert-green)
![Language](https://img.shields.io/badge/Language-Python-blue)
![License](https://img.shields.io/badge/License-MIT-orange)

This project uses GitHub Actions to automatically scrape pollen concentration data from [wetteronline.de](https://www.wetteronline.de/pollen/) and send daily email notifications. Perfect for people with pollen allergies who want to monitor local pollen levels.

🔗 **[Multilingual email templates](https://yliu.tech/projects/pollen-alert-germany/)**

## Features

- 🌱 Automatically fetches pollen forecast data for specified cities
- 📊 Displays concentration levels for different pollen types in an intuitive format
- 📧 Supports multiple email service providers (Gmail, Outlook, Yahoo)
- 🌐 Multi-language support (English, German, and Chinese)
- 🔄 Configurable for daily automatic updates
- 📱 Beautiful HTML email format, mobile-friendly
- 🔧 Highly customizable with command-line arguments and environment variables

## Setup Guide

### 1. Fork this repository

First, click the "Fork" button in the top right corner of this repository to create a copy in your GitHub account.

### 2. Enable GitHub Actions workflow

⚠️ **IMPORTANT**: The workflow is disabled by default. After forking, you need to enable it:

1. Go to your forked repository
2. Click the "Actions" tab
3. Click the "I understand my workflows, go ahead and enable them" button
4. Find the "Pollen Forecast Alert" workflow
5. Click the "Enable workflow" button

### 3. Configure GitHub Secrets

In your forked repository, you need to set up the following GitHub Secrets for email delivery:

1. Go to your forked repository
2. Click "Settings" > "Secrets and variables" > "Actions"
3. Click "New repository secret" and add the following secrets:

**Required secrets:**
- `EMAIL_ADDRESS`: Your email address (**MUST BE Primary Account Address for SMTP login**)
- `RECIPIENT_EMAIL`: The email address that will receive the notifications
- `EMAIL_PASSWORD`: Your email password or app-specific password
- `SMTP_SERVER`: SMTP server address (e.g., smtp.gmail.com)
- `SMTP_PORT`: SMTP server port (e.g., 587 or 465)

**Optional secrets:**
- `CITY_NAME`: City name (default is "berlin")
- `VISIBLE_EMAIL_FROM`: (New) The email address displayed in the "From" header. Use this to set an **alias address** if your `EMAIL_ADDRESS` is the primary account used for login. If not set, it defaults to `EMAIL_ADDRESS`.
- `USE_SSL`: Whether to use SSL connection (true or false)
- `SMTP_AUTH_REQUIRED`: Whether SMTP authentication is required (true or false)
- `SENDER_NAME`: Sender name (default is "Pollen Alert")
- `LANGUAGE`: Email language (en-English, de-German, zh-Chinese)

### 4. Common Email Providers

Here are SMTP settings for some common email providers:

| Provider | SMTP Server | Port | SSL | Auth | Note |
|----------|-------------|------|-----|------|------|
| Gmail | smtp.gmail.com | 587 | false | true | Requires [app password](https://support.google.com/accounts/answer/185833) |
| Outlook | smtp.office365.com | 587 | false | true | |
| Yahoo | smtp.mail.yahoo.com | 587 | false | true | |

### 5. GitHub Actions Configuration

The repository includes a GitHub Actions workflow file (.github/workflows/pollen_scraper.yml) that is set to run automatically at 7:00 AM UTC (8-9 AM Central European Time) every day once enabled.

If you want to modify the run time, you can edit the cron expression in that file:

```yaml
on:
  schedule:
    - cron: '0 7 * * *'  # Runs at 7:00 AM UTC every day
