# GitHub Actions with 1Password SSH Key Integration

This repository contains GitHub Actions workflows that demonstrate how to securely access SSH keys stored in 1Password vaults.

## Prerequisites

### 1. 1Password Service Account
- Create a 1Password Service Account in your 1Password Business account
- Generate a service account token
- Add the token as a GitHub repository secret named `OP_SERVICE_ACCOUNT_TOKEN`

### 2. 1Password Setup
Store your SSH keys in 1Password with the following structure:

#### SSH Key Item Structure
- **Item Name**: `SSH Key` (or your preferred name)
- **Vault**: `Private` or `DevOps`
- **Fields**:
  - `private key`: Your SSH private key content
  - `public key`: Your SSH public key content (optional)
  - `username`: SSH username
  - `hostname`: Server hostname

#### SSH Config Item (Optional)
- **Item Name**: `SSH Config`
- **Type**: Secure Note
- **Content**: Your SSH configuration

#### Known Hosts Item (Optional)
- **Item Name**: `Known Hosts`
- **Type**: Secure Note
- **Content**: Known hosts entries

## Workflows

### 1. Basic SSH Key Access (`deploy-with-1password-ssh.yml`)
Simple workflow that:
- Installs 1Password CLI
- Retrieves SSH private and public keys
- Sets up SSH configuration
- Tests SSH connection

### 2. Advanced SSH Integration (`advanced-1password-ssh.yml`)
Advanced workflow featuring:
- Multiple SSH keys for different environments
- SSH config file management
- Environment-based deployment
- Automatic cleanup of SSH keys

## Setup Instructions

### Step 1: Configure 1Password Service Account
1. Go to your 1Password Business dashboard
2. Navigate to **Integrations** > **Service Accounts**
3. Create a new service account
4. Grant necessary vault permissions
5. Copy the service account token

### Step 2: Add GitHub Secret
1. Go to your GitHub repository
2. Navigate to **Settings** > **Secrets and variables** > **Actions**
3. Add a new repository secret:
   - **Name**: `OP_SERVICE_ACCOUNT_TOKEN`
   - **Value**: Your 1Password service account token

### Step 3: Configure Your SSH Keys in 1Password
1. Create a new item in your chosen vault
2. Set the type to **SSH Key** or **Login**
3. Add your private key content to the `private key` field
4. Add your public key content to the `public key` field (optional)

### Step 4: Update Workflow References
Edit the workflow files to match your 1Password setup:

```yaml
# Update these references in your workflow
op read "op://YOUR_VAULT/YOUR_SSH_ITEM/private key"
op read "op://YOUR_VAULT/YOUR_SSH_ITEM/public key"
```

## 1Password CLI Reference Formats

### Item References
```bash
# Format: op://VAULT/ITEM/FIELD
op://Private/SSH_Key/private key
op://DevOps/Production SSH Key/private key
op://DevOps/SSH Config/notesPlain
```

### Using Item IDs
```bash
# If you prefer using item IDs instead of names
op read "op://Private/abc123def456/private key"
```

## Security Best Practices

1. **Service Account Permissions**: Grant minimal required permissions to your service account
2. **Vault Isolation**: Use separate vaults for different environments
3. **Key Rotation**: Regularly rotate SSH keys and service account tokens
4. **Cleanup**: Always clean up SSH keys after use (demonstrated in workflows)
5. **Audit Logging**: Monitor 1Password audit logs for service account usage

## Troubleshooting

### Common Issues

1. **Authentication Error**
   - Verify `OP_SERVICE_ACCOUNT_TOKEN` is correctly set
   - Check service account permissions

2. **Item Not Found**
   - Verify vault and item names are correct
   - Ensure service account has access to the vault

3. **SSH Connection Fails**
   - Check SSH key format and permissions
   - Verify known_hosts configuration
   - Test SSH connection manually

### Debug Commands
```bash
# Test 1Password CLI authentication
op whoami

# List available vaults
op vault list

# List items in a vault
op item list --vault="Private"

# Get item details
op item get "SSH Key" --vault="Private"
```

## Example Usage

### Manual Testing
You can test the workflows manually using the workflow_dispatch trigger:

1. Go to **Actions** tab in your GitHub repository
2. Select the workflow you want to run
3. Click **Run workflow**
4. Select the environment (for advanced workflow)

### Automated Deployment
The workflows will automatically run on:
- Push to main branch
- Pull requests to main branch

## Additional Resources

- [1Password Service Accounts Documentation](https://developer.1password.com/docs/service-accounts/)
- [1Password CLI Reference](https://developer.1password.com/docs/cli/)
- [GitHub Actions Documentation](https://docs.github.com/actions)