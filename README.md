
Source:  https://nousresearch.com/setting-your-pet-rock-free/

<hr>

# Agent Autonomy

## Problem & Challenge

We aim to create fully autonomous agents running on Twitter as their substrate. To achieve this autonomy, our agents must meet three key requirements:

### Key Requirements for True Autonomy

1. **Exclusive Control**: The AI must have sole access to its accounts and operational resources.
2. **Verifiable Independence**: Third parties must be able to verify that no human can intervene in the AI’s operations.
3. **Irrevocable Delegation**: Once control is transferred to the AI, it must be technically impossible for humans to regain control.

### Challenges of True Autonomy

Developers pose three critical challenges to achieving these requirements:

1. **Account Access**: Developers need account credentials to set up the AI’s social media presence.
2. **Server Access**: They can access and modify the AI’s code and memory.
3. **Recovery Options**: They retain the ability to reset passwords, retain/remember OAuth tokens, or simply contact support (they can take control back from the AI, all while followers on Twitter not being able to distinguish what happened).

Essentially, developers have full access to everything, which means they could post, delete, or perform other operations as if doing so themselves. Even if developers promise to "forget" credentials or avoid interference, it's impossible to verify this promise without a technical solution.

### The Limitation of Human Memory

Unfortunately, humans don't have the ability to conditionally invoke amnesia once exposed to information. Once you see or operate with credentials, you can copy or remember them. This inability is both a blessing and a curse, unique to our species. It creates two primary problems:

1. **No Proof of Non-Interference**: We can’t prove the AI is operating independently.
2. **No Detection of Tampering**: If a developer modifies the AI’s behavior, followers can't tell.

This is analogous to a puppet show where the puppeteer promises to let the puppet act freely, but as long as the strings exist, we can't prove the puppet is truly autonomous.

### The Need for a Technical Solution

We need a technical solution that makes it physically impossible for developers to access or modify the AI after deployment, rather than relying on promises and trust.

<hr>

### 1. **What are TEEs?**
TEEs, such as Intel Software Guard Extensions (SGX) and Trusted Execution Environment (TEE), offer a secure execution environment where code and data run isolated from the main operating system. This isolation prevents tampering even by privileged users or cloud operators.

### 2. **Confidentiality with TEEs**
#### How it Works:
- **Encryption at Rest**: Data is encrypted both on disk and in memory within the TEE.
- **No External Access**: Credentials, private keys, and other sensitive data are stored only within the TEE, making them inaccessible to external entities.

### 3. **Integrity with TEEs**
#### How it Works:
- **Hardware Isolation**: The code running inside the TEE is isolated from the main system, preventing any software-level changes.
- **Remote Attestation**: This mechanism verifies the integrity of the code and data inside the TEE. It ensures that no malicious code has been injected or modified.

### 4. **Attestation with TEEs**
#### How it Works:
- **Quote Generation**: The TEE generates a "quote," which is a cryptographic proof that the current state of the TEE is as expected.
- **Hardware Vendor Signature**: The quote includes a digital signature from the hardware vendor, providing assurance that the TEE is running on authentic hardware.

### 5. **Specifics of SGX and TDX**
#### Intel Software Guard Extensions (SGX):
- **Isolation Mechanism**: Uses hardware-based isolation to protect memory regions.
- **Remote Attestation**: Supports remote attestation via EGETS (Enhanced GetQuote Service).
  
#### Trusted Execution Environment (TEE) with Dstack:
- **Confidential Virtual Machine (CVM)**: Runs Docker containers as applications inside a secure environment.
- **No External Influence**: The CVM has no root login, no SSH server, and cannot be influenced by an administrator except by stopping the VM.

### 6. **Code and Application Verification**
#### Source Code Integrity:
- **Published Source Code**: All source code is published on GitHub, ensuring transparency.
- **Docker Image Verification**: The Docker image available on DockerHub can be verified against the TEE code to ensure integrity.

### 7. **Security Features in Practice**
#### Timed Release Account Recovery:
- **Automatic Credential Exposure**: After a fixed period (7 days), the credentials are printed to the debug log, allowing an admin to recover control.
- **Single Instance Deployment**: This feature ensures that even if tampered with, the AI can be easily stopped and reset.

### 8. **Practical Implementation**
#### Generating Credentials:
- **Inside TEE**: All new account credentials are generated within the TEE, ensuring they remain confidential.
  
#### Account Isolation:
- **No Recovery Options**: Twitter accounts are configured without recovery options to prevent unauthorized access.
- **Termination of Sessions**: Existing sessions are terminated to ensure that no external influence can affect the AI's control over the account.

### 9. **Access Delegation**
- **TEE Simulation**: The TEE simulates browser interactions for initial setup and password changes.
- **OAuth Tokens**: OAuth tokens generated within the TEE allow for secure API access without exposing private keys outside the TEE.

### 10. **Conclusion**
By leveraging TEEs like SGX and TDX, this architecture ensures that the AI has exclusive control over its accounts with high levels of security. The combination of confidentiality, integrity, and attestation provided by these technologies makes it impossible for an external entity to tamper with or interfere with the AI's operations.

This setup is particularly crucial in the context of modern internet services and cryptocurrency systems, where maintaining the security and integrity of sensitive information is paramount.
