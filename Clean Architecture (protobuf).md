## Repository Structure for simple-grpc-api-proto

This repository (`simple-grpc-api-proto`) contains the Protocol Buffer (`.proto`) definitions for the `simple-grpc-api` project. While Clean Architecture is primarily an _application_ architecture, we can apply some of its principles to organize our proto files for clarity, maintainability, and scalability.

**Goal:** To create a structure that is easy to navigate, understand, and extend as the API evolves.

**Top-Level Structure:**

Suggested directory structure for the shared proto files project (using top-level folder versioning):

    simple-grpc-api-proto/
    ├── proto/             # Main directory for all proto files
    │   ├── v1/            # Version 1 of the API
    │   │   ├── user/          # User-related proto definitions
    │   │   │   └── user.proto
    │   │   ├── item/          # Item-related proto definitions
    │   │   │   └── item.proto
    │   │   ├── purchase/      # Purchase-related proto definitions
    │   │   │   └── purchase.proto
    │   │   ├── common/        # Commonly used proto definitions
    │   │   │   └── common.proto
    │   │   └── service.proto  # (Optional) Top-level service definition for v1
    │   ├── v2/            # Version 2 of the API (if needed)
    │   │   ├── user/
    │   │   │   └── user.proto
    │   │   ├── item/
    │   │   │   └── item.proto
    │   │   ├── purchase/
    │   │   │   └── purchase.proto
    │   │   ├── common/
    │   │   │   └── common.proto
    │   │   └── service.proto
    └── README.md          # Documentation for the repository

**Explanation:**

- **`proto/`**: This is the root directory for all proto files. Using a `proto` directory clearly indicates the purpose of this repository.

- **Subdirectories (e.g., `user/`, `item/`, `purchase/`)**: We organize proto files by domain or bounded context. This aligns with the Clean Architecture principle of organizing code by feature or business functionality.

  - `user/user.proto`: Contains the proto definitions for the `User` service and related messages (e.g., `User`, `CreateUserRequest`, `CreateUserResponse`, `GetUserRequest`, etc.).
  - `item/item.proto`: Contains the proto definitions for the `Item` service and related messages.
  - `purchase/purchase.proto`: Contains the proto definitions for the `Purchase` service and related messages.

- **`common/`**: This directory is for proto definitions that are used across multiple services or domains.

  - `common/common.proto`: Might contain reusable message definitions like `ErrorResponse`, `PaginationRequest`, or other general-purpose messages. This avoids duplication.

- **`service.proto` (Optional)**: In some cases, you might have a top-level `service.proto` file that imports all the individual service-specific proto files. This can be useful for defining the overall API structure or for code generation tools. Whether to use this is a matter of style and project needs. This folder can be omitted if the implemented services are very independent.

- **`README.md`**: This file provides essential documentation for the repository:
  - A description of the API.
  - How to use the proto files (e.g., how to generate code).
  - Versioning information.
  - Contact information for API owners.

**Why this structure?**

- **Clarity and Organization:** It's easy to find the proto definitions for a specific domain.
- **Maintainability:** Changes to the `User` API only affect the files in the `user/` directory.
- **Scalability:** As the API grows, you can add new directories for new domains or services without making the structure unwieldy.
- **Reusability:** The `common/` directory promotes the reuse of proto definitions, reducing redundancy.
- **Alignment with Clean Architecture:** While not a direct mapping, this structure aligns with the idea of organizing code by business functionality, making the API definition easier to understand for developers working on different parts of the system.

**Versioning:**

- This structure uses directory-based versioning. Each major version of the API has its own directory (e.g., `v1`, `v2`) under `proto/`.

  - **Major Version Change:** When there are breaking changes, a new top-level versioned directory is created (e.g., `v2`).
  - **Minor/Patch Changes:** Non-breaking changes can be handled within the same versioned directory by adding new fields, messages, or services.

- Package names in the proto files should also reflect the version:

  - Example: `package com.example.user.v1;`

- For accessing private repositories, SSH keys can be used to establish a secure connection between your services and the repository. This involves generating an SSH key pair (a public key and a private key) on the machine where your service will run. The public key is then added to your GitHub account or the specific private repository, while the private key is kept secret and used by your service to authenticate. This allows your service to clone or fetch the proto files without needing to provide a username and password.

This structure provides a robust way to manage API versions in your `simple-grpc-api-proto` repository. The explicit versioning at the directory level makes it clear how your API evolves and simplifies the process of supporting multiple versions.
