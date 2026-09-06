# Leak Shield Bot

A Python-based GitHub webhook listener that automatically detects leaked AWS access keys in your commits, verifies if they are live, and revokes them immediately to prevent unauthorized access.

## Features
- **Webhook Listener**: Listens for GitHub push events.
- **Secret Scanning**: Scans newly added or modified files for potential secrets using Regex (e.g., AWS Access Keys, Stripe Keys, Slack Tokens).
- **Verification**: Automatically tests leaked AWS Access Keys to confirm they are active before taking action.
- **Auto-Revocation**: Deactivates the leaked AWS key via IAM if it is verified as live.
- **Slack Notifications**: Sends alerts about detected secrets and automated actions taken.

## Setup
1. Clone this repository.
2. Install dependencies: `pip install -r requirements.txt`
3. Create a `.env` file based on your credentials (make sure it's not committed!):
   ```
   ADMIN_AWS_ACCESS_KEY=your_admin_access_key
   ADMIN_AWS_SECRET_KEY=your_admin_secret_key
   DEMO_LEAKED_SECRET_KEY=secret_for_demo_key
   SLACK_WEBHOOK_URL=your_slack_webhook
   ```
4. Run the application: `python app.py`

## Limitations (Demo Mode)
* This is currently a prototype/demo version.
* It expects a specific demo IAM user (`demo-leak-user`) to revoke the key from.
* It verifies using a predefined demo secret key.

## Disclaimer
Do NOT use this directly in production without adapting the IAM user lookup and adding webhook signature verification.
