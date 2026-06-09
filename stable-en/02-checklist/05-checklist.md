---

layout: col-document
title: Secure Coding Practices
tags: SCP-QRG
document: OWASP Secure Coding Practices - Quick Reference Guide

---

{% include breadcrumb.html %}

**Version:** 1.0  
**Last Updated:** 09 June 2026

# Secure Coding Practices Checklist

This checklist provides a consolidated set of secure coding requirements 
designed to reduce common vulnerabilities across modern applications. 
It aligns with OWASP guidance and supports developers, reviewers, and 
security engineers in implementing consistent, high‑assurance controls.

## Table of Contents
- [1. Input validation](#1-input-validation)
- [2. Output encoding](#2-output-encoding)
- [3. Authentication and password management](#3-authentication-and-password-management)
- [4. Session management](#4-session-management)
- [5. Access control](#5-access-control)
- [6. Cryptographic practices](#6-cryptographic-practices)
- [7. Error handling and logging](#7-error-handling-and-logging)
- [8. Data protection](#8-data-protection)
- [9. Communication security](#9-communication-security)
- [10. System configuration](#10-system-configuration)
- [11. Database security](#11-database-security)
- [12. File management](#12-file-management)
- [13. Memory management](#13-memory-management)
- [14. General coding practices](#14-general-coding-practices)

## 1. Input validation

- [ ] Perform all input validation on a trusted system (server‑side, not client‑side).

- [ ] Identify all data sources and classify them as trusted or untrusted.

- [ ] Validate all data originating from untrusted sources, including databases, file streams, and external systems.

- [ ] Use a centralized input validation routine across the application.

- [ ] Define and enforce expected character sets (e.g., UTF‑8) for all input sources.

- [ ] Normalize input to a consistent character set before validating.

- [ ] Reject input whenever validation checks fail.

- [ ] Validate only after UTF‑8 decoding is complete when extended character sets are supported.

- [ ] Validate all client‑provided data before processing.

- [ ] Ensure protocol header values in requests and responses contain only ASCII characters.

- [ ] Validate data received through redirects.

- [ ] Validate input using allowlists for expected data types rather than denylists.

- [ ] Validate data ranges.

- [ ] Validate data lengths.

- [ ] Apply additional controls when potentially hazardous input must be accepted.

- [ ] Use discrete, specialized checks when standard validation routines cannot fully address certain inputs.

- [ ] Apply canonicalization to mitigate obfuscation attacks.

## 2. Output encoding

- [ ]   Conduct all output encoding on a trusted system (server side not client side)

- [ ]   Utilize a standard, tested routine for each type of outbound encoding

- [ ]   Specify character sets, such as UTF-8, for all outputs

- [ ]   Contextually output encode all data returned to the client from untrusted sources

- [ ]   Ensure the output encoding is safe for all target systems

- [ ]   Contextually sanitize all output of un-trusted data to queries for SQL, XML, and LDAP

- [ ]   Sanitize all output of untrusted data to operating system commands

## 3. Authentication and password management

- [ ] Require authentication for all pages and resources except those explicitly intended to be public.

- [ ] Enforce all authentication controls on a trusted system.

- [ ] Use standard, well‑tested authentication services whenever possible.

- [ ] Centralize all authentication logic, including libraries that call external authentication services.

- [ ] Separate authentication logic from requested resources and use redirection to and from centralized authentication controls.

- [ ] Ensure all authentication controls fail securely.

- [ ] Ensure administrative and account‑management functions are protected with controls at least as strong as primary authentication.

- [ ] Use cryptographically strong, one‑way salted hashes when managing a credential store.

- [ ] Perform password hashing only on a trusted system (server‑side).

- [ ] Validate authentication data only after all required input has been received.

- [ ] Ensure authentication failure responses do not reveal which part of the credentials was incorrect.

- [ ] Require authentication for connections to external systems involving sensitive information or functions.

- [ ] Store authentication credentials for external services in a secure credential store.

- [ ] Use only HTTP POST requests to transmit authentication credentials.

- [ ] Transmit non‑temporary passwords only over encrypted channels or as encrypted data.

- [ ] Enforce password complexity requirements defined by policy or regulation.

- [ ] Enforce password length requirements defined by policy or regulation.

- [ ] Obscure password entry on the user’s screen.

- [ ] Disable accounts after a defined number of invalid login attempts.

- [ ] Apply the same security controls to password reset and password change operations as to account creation and authentication.

- [ ] Ensure password reset questions support sufficiently random and unpredictable answers.

- [ ] For email‑based resets, send reset links or temporary passwords only to pre‑registered addresses.

- [ ] Ensure temporary passwords and reset links have short expiration times.

- [ ] Require temporary passwords to be changed on next use.

- [ ] Notify users when a password reset occurs.

- [ ] Prevent password reuse according to policy.

- [ ] Enforce a minimum password age to reduce rapid password‑cycling attacks.

- [ ] Enforce periodic password changes only when required by policy or regulation.

- [ ] Disable “remember me” functionality for password fields.

- [ ] Display the last successful or unsuccessful login time to the user after authentication.

- [ ] Implement monitoring to identify attacks against multiple user accounts, especially those using the same password.
     
## 4. Session management

- [ ] Use only the server or framework’s built‑in session management controls, and recognize only those session identifiers as valid.

- [ ] Create all session identifiers on a trusted system (server‑side).

- [ ] Use well‑vetted algorithms that generate sufficiently random and unpredictable session identifiers.

- [ ] Set cookie domain and path attributes to the most restrictive values appropriate for the application.

- [ ] Ensure logout functionality fully terminates the associated session or connection.

- [ ] Provide logout functionality on all pages that require authorization.

- [ ] Configure session inactivity timeouts to be as short as practical while balancing business requirements.

- [ ] Disallow persistent logins and enforce periodic session termination, even during active use.

- [ ] Close any pre‑login session and establish a new session after successful authentication.

- [ ] Generate a new session identifier upon any re‑authentication event.

- [ ] Prevent concurrent logins using the same user ID.

- [ ] Do not expose session identifiers in URLs, error messages, or logs.

- [ ] Implement access controls to protect server‑side session data from unauthorized access by other users of the server.

- [ ] Periodically generate a new session identifier and deactivate the old one.

- [ ] Generate a new session identifier when connection security changes (e.g., HTTP → HTTPS).

- [ ] Use HTTPS consistently rather than switching between HTTP and HTTPS.

- [ ] Supplement standard session management for sensitive operations with

## 5. Access control

- [ ] Use only trusted server‑side objects (e.g., session objects) when making authorization decisions.

- [ ] Use a single, centralized component to enforce access authorization, including libraries that call external authorization services.

- [ ] Ensure all access control mechanisms fail securely.

- [ ] Deny all access if the application cannot retrieve its security configuration.

- [ ] Enforce authorization checks on every request, including those made by server‑side scripts or background processes.

- [ ] Segregate privileged logic from non‑privileged application code.

- [ ] Restrict access to files and resources—including those outside the application’s direct control—to authorized users only.

- [ ] Restrict access to protected URLs to authorized users.

- [ ] Restrict access to protected functions to authorized users.

- [ ] Restrict direct object references to authorized users.

- [ ] Restrict access to internal services to authorized users.

- [ ] Restrict access to application data to authorized users.

- [ ] Restrict access to user attributes, data attributes, and policy information used in authorization decisions.

- [ ] Restrict access to security‑relevant configuration information to authorized users.

- [ ] Ensure server‑side implementation of access control rules matches the presentation‑layer representation.

- [ ] When client‑side state must be stored, use server‑side integrity checks and encryption to detect tampering.

- [ ] Enforce application logic flows to comply with defined business rules.

- [ ] Limit the number of transactions a user or device can perform within a defined period to deter automated attacks.

- [ ] Use the “Referer” header only as a supplemental check; never rely on it as the sole authorization mechanism.

- [ ] For long‑lived authenticated sessions, periodically re‑validate user authorization and terminate the session if privileges have changed.

- [ ] Implement account auditing and disable unused accounts.

- [ ] Ensure the application supports disabling accounts and terminating sessions when authorization ceases.

- [ ] Assign the least privilege possible to service accounts or accounts used for external system connections.

- [ ] Maintain an Access Control Policy documenting business rules, data types, authorization criteria, and provisioning processes for both data and system resources.

## 6. Cryptographic practices

- [ ] Implement all cryptographic functions on a trusted system to protect secrets from unauthorized access.

- [ ] Protect all secrets from unauthorized disclosure, modification, or misuse.

- [ ] Ensure cryptographic modules fail securely.

- [ ] Generate all random numbers, random file names, random GUIDs, and random strings using an approved cryptographic random number generator.

- [ ] Use cryptographic modules that comply with FIPS 140‑2 or an equivalent standard.

- [ ] Establish and follow a documented policy and process for cryptographic key management, including generation, distribution, rotation, storage, and destruction.

## 7. Error handling and logging

- [ ] Do not disclose sensitive information in error responses, including system details, session identifiers, or account information.

- [ ] Use error handlers that do not display debugging information or stack traces.

- [ ] Provide generic error messages and use custom error pages.

- [ ] Ensure the application handles its own errors rather than relying on server configuration defaults.

- [ ] Properly release allocated memory and resources when error conditions occur.

- [ ] Ensure error‑handling logic associated with security controls denies access by default.

- [ ] Implement all logging controls on a trusted system.

- [ ] Log both successful and failed security‑relevant events.

- [ ] Ensure logs contain sufficient detail to support security monitoring and forensic analysis.

- [ ] Ensure log entries containing untrusted data cannot be executed as code in log viewers or analysis tools.

- [ ] Restrict access to logs to authorized individuals only.

- [ ] Use a centralized routine for all logging operations.

- [ ] Do not store sensitive information in logs, including passwords, session identifiers, or unnecessary system details.

- [ ] Ensure a mechanism exists to perform regular log analysis.

- [ ] Log all input validation failures.

- [ ] Log all authentication attempts, especially failures.

- [ ] Log all access control failures.

- [ ] Log all apparent tampering events, including unexpected changes to state data.

- [ ] Log attempts to use invalid or expired session tokens.

- [ ] Log all system exceptions.

- [ ] Log all administrative actions, including changes to security configuration settings.

- [ ] Log all backend TLS connection failures.

- [ ] Log cryptographic module failures.

- [ ] Use cryptographic hash functions to protect log integrity and detect tampering.

## 8. Data protection

- [ ] Implement least privilege by restricting users to only the functionality, data, and system information required to perform their tasks.

- [ ] Protect all cached or temporary copies of sensitive data stored on the server from unauthorized access, and securely purge temporary files as soon as they are no longer required.

- [ ] Encrypt highly sensitive stored information, including authentication verification data, even when stored on the server side.

- [ ] Prevent server‑side source code from being downloaded or exposed to users.

- [ ] Do not store passwords, connection strings, or other sensitive information in clear text or in any non‑cryptographically secure manner on the client side.

- [ ] Remove comments in production code that may reveal backend system details or other sensitive information.

- [ ] Remove unnecessary application and system documentation that could provide useful information to attackers.

- [ ] Do not include sensitive information in HTTP GET request parameters.

- [ ] Disable autocomplete features on forms that contain sensitive information, including authentication fields.

- [ ] Disable client‑side caching on pages that display or process sensitive information.

- [ ] Ensure the application supports secure removal of sensitive data when it is no longer required.

- [ ] Implement appropriate access controls for sensitive data stored on the server, including cached data, temporary files, and data intended only for specific system users.

## 9. Communication security

- [ ] Implement encryption for the transmission of all sensitive information, including the use of TLS to protect connections. Supplement TLS with additional encryption for sensitive files or non‑HTTP protocols when required.

- [ ] Ensure TLS certificates are valid, correctly bound to the domain name, unexpired, and installed with all required intermediate certificates.

- [ ] Prevent insecure fallback by ensuring failed TLS connections do not revert to unencrypted communication.

- [ ] Use TLS for all authenticated content and for all transmissions involving sensitive information.

- [ ] Use TLS for all connections to external systems that handle sensitive information or perform sensitive operations.

- [ ] Standardize on a single, well‑configured TLS implementation across the application.

- [ ] Specify character encodings for all connections to ensure consistent and secure data handling.

- [ ] Filter or remove sensitive information from HTTP Referer headers when linking to external sites.

## 10. System configuration

- [ ] Ensure all servers, frameworks, and system components run the latest approved versions.

- [ ] Apply all security patches for the versions in use and maintain an established patch‑management process.

- [ ] Disable directory listings on all web servers.

- [ ] Restrict web server, process, and service accounts to the least privileges required.

- [ ] Ensure all components fail securely when exceptions occur.

- [ ] Remove all unnecessary functionality, services, and files from production systems.

- [ ] Remove test code, debugging utilities, and any functionality not intended for production before deployment.

- [ ] Prevent disclosure of directory structures in robots.txt by placing non‑public directories under an isolated parent directory.

- [ ] Define which HTTP methods (e.g., GET, POST) the application supports and enforce method restrictions per page or endpoint.

- [ ] Disable all unnecessary HTTP methods.

- [ ] Ensure consistent configuration across all supported HTTP protocol versions and understand any differences.

- [ ] Remove unnecessary information from HTTP response headers, including OS details, web server versions, and framework identifiers.

- [ ] Ensure the application’s security configuration store can be exported in a human‑readable format for auditing.

- [ ] Implement an asset management system and register all system components and software.

- [ ] Isolate development and testing environments from the production network and restrict access to authorized personnel only.

- [ ] Implement a software change‑control system to manage and record changes to code in both development and production environments.

## 11. Database security

- [ ] Use strongly typed, parameterized queries for all database interactions.

- [ ] Apply input validation and output encoding to all data sent to the database, and block execution if validation fails.

- [ ] Ensure all variables used in database operations are strongly typed.

- [ ] Access the database using the lowest level of privilege required for the operation.

- [ ] Use secure, protected credentials for all database connections.

- [ ] Do not hard‑code connection strings in the application. Store them in a secure configuration file on a trusted system, and encrypt them.

- [ ] Use stored procedures to abstract data access and remove direct permissions to base tables.

- [ ] Close database connections as soon as operations are complete.

- [ ] Remove or change all default administrative passwords for the database.

- [ ] Disable all unnecessary database functionality and services.

- [ ] Remove unnecessary default vendor content, such as sample schemas or test data.

- [ ] Disable any default accounts not required to support business operations.

- [ ] Use separate database credentials for each trust level (e.g., standard user, read‑only user, guest, administrator).

## 12. File management

- [ ] Do not pass user‑supplied data directly to any dynamic include or file‑execution function.

- [ ] Require authentication before allowing any file upload.

- [ ] Restrict uploadable file types to only those required for business purposes.

- [ ] Validate uploaded files by inspecting file headers or MIME types rather than relying on file extensions.

- [ ] Store uploaded files outside the web‑accessible directory structure.

- [ ] Prevent or restrict the uploading of any file type that could be interpreted or executed by the web server.

- [ ] Disable execution privileges on all file‑upload directories.

- [ ] Implement safe file‑upload handling in UNIX environments by mounting the upload directory as a logical drive or using a chrooted environment.

- [ ] When referencing existing files, use an allow‑list of permitted file names and types.

- [ ] Do not pass user‑supplied data into dynamic redirects.

- [ ] Do not accept directory or file paths from users; instead, map index values to predefined, validated paths.

- [ ] Never send absolute file paths to the client.

- [ ] Ensure application files and resources are read‑only wherever possible.

- [ ] Scan all user‑uploaded files for viruses and malware before processing or storage.

## 13. Memory management

- [ ] Apply strict input and output controls when handling untrusted data.

- [ ] Ensure all buffers are sized correctly and validated before use.

- [ ] When using functions that accept a byte count, ensure NULL termination is handled safely and explicitly.

- [ ] Validate buffer boundaries during loops or repeated operations to prevent overflow conditions.

- [ ] Truncate all input strings to a reasonable, predefined length before passing them to other functions.

- [ ] Explicitly close all resources when they are no longer needed; do not rely solely on garbage collection.

- [ ] Use non‑executable stacks and memory protections when supported by the platform.

- [ ] Avoid using functions known to be vulnerable or unsafe.

- [ ] Free allocated memory properly upon function completion and at all exit points.

- [ ] Overwrite sensitive information stored in memory before freeing it to prevent data leakage.

## 14. General coding practices

- [ ] Use tested and approved managed code whenever possible instead of creating new unmanaged code for common tasks.

- [ ] Use task‑specific, built‑in APIs to perform operating system operations. Avoid issuing direct OS commands, especially through application‑initiated command shells.

- [ ] Use checksums or cryptographic hashes to verify the integrity of interpreted code, libraries, executables, and configuration files.

- [ ] Use locking or synchronization mechanisms to prevent race conditions and ensure safe handling of concurrent requests.

- [ ] Protect shared variables and resources from improper concurrent access.

- [ ] Explicitly initialize all variables and data stores during declaration or immediately before first use.

- [ ] When elevated privileges are required, raise privileges as late as possible and drop them as soon as they are no longer needed.

- [ ] Prevent calculation errors by understanding the underlying numeric representation and behavior of the programming language.

- [ ] Do not pass user‑supplied data to any dynamic execution function (e.g., eval, exec).

- [ ] Restrict users from generating new code or modifying existing code within the application.

- [ ] Review all secondary applications, third‑party code, and libraries to confirm business necessity and validate safe functionality.

- [ ] Implement secure update mechanisms that use encrypted channels and verify update integrity.



