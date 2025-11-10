# Security

Describes how users are authenticated and authorized to ensure each can securely access only their own data.

---

## Authentication Flow

```mermaid
flowchart TD
    A(["Start"]) --> B{"Do you have an account?"}
    B -- Yes --> C["Login Page"]
    B -- No --> D["Register Page"]
    C --> E["Enter Username and Password"]
    E --> F{"Credentials Valid?"}
    F -- Yes --> G["Access Granted - Redirect to Dashboard"]
    F -- No --> H["Show Error Message - Retry Option"]
    H --> I{"Forgot Password?"}
    I -- Yes --> J["Go to Forgot Password Page"]
    I -- No --> E
    D --> K["Enter Details: Name, Email, Password"]
    K --> L["Validate Input"]
    L -- Valid --> M["Create Account"]
    L -- Invalid --> N["Show Error Message"]
    M --> O["Account Created Successfully"]
    O --> C
    J --> P["Enter Registered Email"]
    P --> Q["Send Password Reset Link"]
    Q --> R["Check Email for Reset Link"]
    R --> S["Set New Password"]
    S --> T["Password Updated Successfully"]
    T --> C
    G --> U(["End"])

    E@{ shape: lean-r}
    K@{ shape: lean-r}
    L@{ shape: diam}
```