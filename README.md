# Firefly Framework - IDP - Azure AD

[![CI](https://github.com/fireflyframework/fireflyframework-idp-azure-ad/actions/workflows/ci.yml/badge.svg)](https://github.com/fireflyframework/fireflyframework-idp-azure-ad/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21%2B-orange.svg)](https://openjdk.org)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)

> Azure AD (Entra ID and B2C) implementation of the Firefly IDP adapter for user management and authentication.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

Firefly Framework IDP Azure AD implements the `IdpAdapter` interface using Microsoft Entra ID (formerly Azure Active Directory) and Azure AD B2C as the identity provider. It provides user management, authentication, token operations, and role management through MSAL4J and the Microsoft Graph SDK.

The module includes `AzureAdIdpAdapter` as the main adapter implementation, backed by `AzureAdAuthService` for authentication operations (login, refresh, logout, introspection, user info) and a strategy-based admin layer with `EntraIdAdminService` and `B2CAdminService` for administrative functions. The active admin service is selected automatically based on the configured mode (`entra-id` or `b2c`).

## Features

- Full `IdpAdapter` implementation supporting both Entra ID and Azure AD B2C
- User creation, update, and password management via Microsoft Graph API
- Authentication with username/password (ROPC flow) and token refresh via MSAL4J
- Strategy-based admin service selection (Entra ID or B2C) via configuration
- Configurable role mapping strategy (app roles, security groups, or both)
- Configurable Graph client and MSAL client factories with timeout support
- Local JWT introspection and user info retrieval via Graph API
- Configurable via `AzureAdProperties`

## Requirements

- Java 21+
- Spring Boot 3.x
- Maven 3.9+
- Azure AD tenant with an app registration configured

## Installation

```xml
<dependency>
    <groupId>org.fireflyframework</groupId>
    <artifactId>fireflyframework-idp-azure-ad</artifactId>
    <version>26.02.07</version>
</dependency>
```

## Quick Start

```xml
<dependencies>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-idp</artifactId>
    </dependency>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-idp-azure-ad</artifactId>
    </dependency>
</dependencies>
```

## Configuration

### Entra ID (default)

```yaml
firefly:
  idp:
    provider: azure-ad
    azure-ad:
      mode: entra-id
      tenant-id: your-tenant-id
      client-id: your-client-id
      client-secret: your-client-secret
      role-mapping:
        strategy: app-roles        # "app-roles", "groups", or "both"
        group-prefix: ""
      connection-timeout: 30000
      request-timeout: 60000
```

### Azure AD B2C

```yaml
firefly:
  idp:
    provider: azure-ad
    azure-ad:
      mode: b2c
      tenant-id: your-tenant-id
      client-id: your-client-id
      client-secret: your-client-secret
      b2c:
        domain: your-tenant.b2clogin.com
        sign-up-sign-in-policy: B2C_1_signup_signin
        reset-password-policy: B2C_1_password_reset
      role-mapping:
        strategy: groups
        group-prefix: ""
```

## Documentation

No additional documentation available for this project.

## Contributing

Contributions are welcome. Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details on our code of conduct, development process, and how to submit pull requests.

## License

Copyright 2024-2026 Firefly Software Foundation.

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
