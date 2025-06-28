# JWT Toolkit

An toolkit for forging, decoding, and managing JSON Web Tokens (JWTs), specifically designed to streamline testing for `alg=none` / HMAC key confusion vulnerabilities in bug bounty programs.

`NOTE: I used some help of AI to make this`

## Access the Tool

Go to this website and you are ready to go!:

Happy hacking!

**https://ram17722.github.io/JWT-Creator-Tool/**

## Why This Tool?

While hunting for bugs, I often found myself needing to quickly forge JWTs to test for common misconfigurations, particularly the HMAC key confusion attack. This toolkit was built to bring all the necessary features into a single, easy-to-use interface, saving time and effort during security assessments.

## Key Features

-  **Dual Mode: JWT Forger & Decoder**
    
    - Seamlessly switch between building custom JWTs from scratch and decoding existing ones to analyze their structure.
        
-  **Vulnerability-Focused Design**
    
    - Specifically designed to demonstrate and test the **HMAC key confusion vulnerability**. It allows you to provide a public key, which is then used as the secret to sign the token with the `HS256` algorithm.
        
-  **History Management**
    
    - Automatically saves a history of all generated tokens to your browser's local storage.
        
    - View, import, and export your testing history as a JSON file, making it easy to manage your work across sessions.
        
-  **Workflow Enhancements**
    
    - Quickly populate data with one-click header and payload templates.
        
    - Copy generated tokens or send a decoded token's data directly back to the forger for quick modifications.
        

## How It Works: The HMAC Key Confusion Attack

This tool makes it simple to test for a common JWT misconfiguration where a server expects a token signed with an asymmetric algorithm (like `RS256`) but can be tricked into verifying it with a symmetric one (like `HS256`).

1. An attacker obtains the public key used to verify `RS256` signatures.
    
2. The attacker modifies the JWT header, changing the algorithm from `RS256` to `HS256`.
    
3. The attacker then signs the token using the `HS256` algorithm, but instead of a typical secret, they use the **entire public key** as the secret key.
    
4. If the server is misconfigured, its JWT library will see the `HS256` `alg`, fetch what it _thinks_ is the secret key (which is actually the public key), and successfully validate the forged token.
    

This toolkit automates step 3, allowing you to forge any payload you want.

## Contributing

Contributions, issues, and feature requests are welcome! If you have an idea to improve the tool or want to see a new feature implemented, please feel free to open an issue.

I built this tool to solve my own problems, but I hope it can help others in the bug bounty community too.
