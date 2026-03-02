---
title: MFA integration
layout: doc
nav_order: 5
---

# Multi-factor authentication integration

This integration adds multi-factor authentication (MFA) to an existing OAuth 2.0 login flow. It introduces a second verification step during sign-in and requires backend validation of issued tokens before granting access to protected resources.

---

## What this integration does

The application continues to use the Authorization Code flow. When MFA is enabled, the identity provider may require users to complete an additional verification step before issuing an authorization code.

The identity provider manages second-factor verification and policy enforcement. The application integrates with the updated authentication flow and validates issued tokens before granting access.

---

## How the login flow changes

The MFA step extends the existing OAuth Authorization Code flow and adds an additional verification step before the identity provider issues an authorization code.

The login flow includes the following steps:

1. The application redirects the user to the authorization endpoint.  
2. The identity provider evaluates the configured MFA policy for the user or application.  
3. If the policy requires additional verification, the user completes the second-factor challenge (for example, TOTP or SMS verification).  
4. After successful verification, the identity provider issues an authorization code.  
5. The backend exchanges the authorization code for tokens.  
6. The backend validates the returned access token before granting access.  

Validate tokens by verifying the signature, expiration (`exp`), issuer (`iss`), and audience (`aud`) claims.

---

## What you need to configure

Before enabling MFA:

- Register the application with the identity provider.  
- Configure redirect URIs exactly as defined in the identity provider settings.  
- Generate a Client ID and Client Secret.  

Define the following values in the application configuration:

- Client ID  
- Client Secret  
- Authorization endpoint  
- Token endpoint  
- Redirect URI  

Store credentials securely using environment variables or a secret management system. Do not hardcode credentials or expose them in logs.
