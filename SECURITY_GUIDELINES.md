# Security Guidelines for Implementing Safe Repository Practices using Git

## Table of Contents

- [Introduction](#introduction)
- [Enable Two-Factor Authentication (2FA)](#enable-two-factor-authentication-2fa)
- [Enforce SSH Keys](#enforce-ssh-keys)
- [Implement Role-Based Access Control (RBAC)](#implement-role-based-access-control-rbac)
- [SSH Key Usage](#ssh-key-usage)
- [Conclusion](#conclusion)

## Introduction

Implementing secure practices for repositories involves several key steps, including enabling two-factor authentication (2FA), enforcing SSH keys, and implementing role-based access control (RBAC). Here’s a step-by-step guide to implementing these practices:

## Enable Two-Factor Authentication (2FA)

### Why

Enabling 2FA adds an extra layer of security by requiring users to provide a second form of authentication, such as a code from a security app, in addition to their password.

### How

- **Access GitHub Account Settings**:

  - Log into your GitHub account.

  - Navigate to your account settings.

- **Enable 2FA**:

  - Go to "Password and authentication."

  - Scroll down to "Two-factor authentication" and click "Enable two-factor authentication."

  - Choose your preferred method (e.g., Authenticator App, Security Keys).

  - Follow the prompts to set up 2FA.

## Enforce SSH Keys

### Why

Enforcing SSH keys provides a more secure way to authenticate users and reduce the risk of password theft. It enhances the security of your repositories by ensuring that only authorized users can access them.

### How

- **Generate SSH Keys**:

  - Open a terminal or command prompt.

  - Run the following command:

    ```bash
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```

- **Add SSH Key to ssh-agent**:

  - **Unix environment**:

    - Evaluate and add the ssh-agent:

    ```bash
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519
    ```

    - Copy the public key:

    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```

  - **MS DOS environment**:

    - Start the ssh-agent in the background:

    ```bash
    start-ssh-agent.cmd
    ```

    - Go the directory where your private key has just been stored:

    ```bash
    cd C:\Users\[username]\.ssh
    ```

    - View the content of the directory and verify our private key has been stored:

    ```bash
    dir
    ```

    - Look for a file with the `.pub` extension in the directory. You should get something alike:

    ```bash
    id_ed25519.pub
    ```

    - Open the public key file with any text editor, in order to copy its content:

    ```bash
    notepad id_ed25519.pub
    ```

- **Add SSH Key to GitHub**:

  - Go to your GitHub account settings.

  - Navigate to "SSH and GPG keys".

  - Click "New SSH key".

  - Paste your public key and give it a title.

  - Click "Add SSH key".

## Implement Role-Based Access Control (RBAC)

### Why

Implementing RBAC helps in managing access to repositories by assigning specific permissions to users based on their roles, reducing the risk of unauthorized access and changes.

### How

- **Create Teams and Roles**:

  - In your GitHub organization, create teams (e.g., Developers, Reviewers, Security).

  - Assign roles with specific permissions (e.g., write, maintain, admin).

- **Configure Repository Access**:

  - Set access levels for each repository (e.g., protected branches).

  - Use JSON to define protection rules for branches, including required reviews and status checks2.

  - Assign teams to repositories with specific permissions.

  - Configure branch protection rules:

    - Set required approvals for protected branches.

    - Enable required status checks.

    - Configure required reviews for pull requests.

    - Set branch permissions for each team.

## SSH Key Usage

Now that you have generated and added your SSH key to GitHub, here's how you can use it to connect to securely:

### 1. Cloning a repository via SSH

To clone a repository using SSH, you need to use the SSH URL of the repository. Here’s how you can do it:

- **Find the SSH URL**:

  - Go to the repository on GitHub.

  - Click the "Code" button.

  - Select "SSH" from the dropdown menu.

  - Copy the SSH URL (it should look something like git@github.com:username/repository.git).

- **Clone the Repo**:

  - Open PowerShell or Command Prompt.

  - Navigate to the directory where you want to clone the repository.

  - Run the following command to clone the repository using SSH:

  ```bash
  git clone git@github.com:username/repository.git
  ```

### 2. Push Changes using SSH

After cloning, you can push changes to the repository using SSH, following these steps:

- **Make changes**:

  - Edit files in your local repo

- **Stage and commit changes**:

```bash
git add .
git commit -m "Your commit message"
```

- **Push changes**:

```bash
git push -u origin <branch_name>
```

Replace branch-name with the name of your branch.

### Test your SSH Connection

To ensure your SSH connection is working correctly, you can test it by running:

```bash
ssh -T git@github.com
```

If everything is set up correctly, you should see a message indicating that you've successfully authenticated.

#### Troubleshooting

If you encounter issues, ensure that:

- Your SSH key is correctly added to your GitHub account.

- The SSH key is added to the SSH agent (ssh-add ~/.ssh/id_rsa or ssh-add ~/.ssh/id_ed25519).

- You are using the correct SSH URL for cloning and pushing.

#### Additional Tips

- **Use Git Bash or WSL**: For a more Unix-like experience, consider using Git Bash or Windows Subsystem for Linux (WSL) for Git operations.

- **Keep Your SSH Keys Secure**: Always keep your private SSH key secure and never share it publicly.

## Conclusion

By implementing these practices and leveraging GitHub’s advanced security features, you can significantly enhance the security of your repositories and protect your code from unauthorized access and vulnerabilities.

## Credits

- **Dr BUGINGO Emmanuel**, our lecturer who allowed us to work on this topic
- **Alain MUGISHA**, Group 11 member
- <a href="https://cuttypiedev.vercel.app" target="_blank">Matheo OKISSI</a>, Group 11 member
