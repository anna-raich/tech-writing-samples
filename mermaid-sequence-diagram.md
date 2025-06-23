# Description
This is a Mermaid sequence diagram that outlines a typical OAuth login flow (e.g. “Log in with Google” or “Log in with Facebook”) from a backend perspective showing the interactions between the User, Frontend, Backend, OAuth Provider, and Database.

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant OAuthProvider
    participant Backend
    participant Database

    User->>Frontend: Clicks "Login with OAuth"
    Frontend->>OAuthProvider: Redirects to auth URL
    OAuthProvider->>User: Login & permission consent
    OAuthProvider->>Frontend: Redirect with auth code
    Frontend->>Backend: Send auth code

    Backend->>OAuthProvider: Exchange code for access token
    OAuthProvider-->>Backend: Return access token (and ID token)

    Backend->>OAuthProvider: Fetch user profile
    OAuthProvider-->>Backend: Return user profile

    Backend->>Database: Check if user exists
    alt User exists
        Database-->>Backend: Return user data
        Backend->>Frontend: Generate & return session/token
    else New user
        Backend->>Database: Create new user
        Database-->>Backend: Confirmation
        Backend->>Frontend: Generate & return session/token
    end
```
