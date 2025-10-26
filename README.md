# Experiments repo

If I need to do stuff in GitHub Actions and don't know exactly how to do it, that I will try it first in this repo., wehere I don't know exacly how to do it. 


## List of experiments

- [Use 1Password CLI and service account to get a SSH key](#1password-cli-ssh)

## 1Password CLI SSH

1. **Create a 1Password Service Account** and get the token
2. **Add the token** as `OP_SERVICE_ACCOUNT_TOKEN` in your GitHub repository secrets
3. **Store your SSH key** in 1Password (vault: `Private`, item: `MySSHKey`)
4. **Run the Simple workflow** to test the integration
5. **Customize** the workflows for your deployment needs

> 💡 **New to this?** Start with `simple-1password-ssh.yml` - it's the easiest way to get up and running!

## Prerequisites

### Password Service Account
- Create a 1Password Service Account in your 1Password Business account
- Generate a service