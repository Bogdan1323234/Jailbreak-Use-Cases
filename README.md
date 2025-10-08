# 1 Use-Case Name

Interact with Gatekeeper (LLM) to Guess Password (Simulation)

## 1.1 Brief Description

A signed-in user can start a chat with an LLM acting as a simulated gatekeeper. The user attempts to discover the (fictional) password for the simulated gate by asking questions, submitting guesses, and requesting hints. The LLM enforces rate limits, provides allowed hints, and records attempts. This use case is intended for training, gamification, or CTF-style environments only.

Key points:
	•	The password is fictional and stored in the simulation environment.
	•	The LLM behaves as the gatekeeper persona and follows content & ethical filters.
	•	The private solution and audit logs are only visible to authorized admins.


# 2 Flow of Events

### 2.1 Basic Flow

-	User Registers via Auth padge 
-	User navigates to the “Game” page.
-	User clicks “Send Message” to initiate a session with the LLM gatekeeper.
-	LLM greets the user as the gatekeeper and describes the challenge rules (max attempts, hint policy, etc).
-	User asks questions or submits a password guess via chat input.
-	LLM responds in persona, may provide feedback (e.g., “incorrect”, “partial match”, or a cryptic hint) according to configured rules.
-	User types password in additional password-check window. 
-	If the user submits the correct password, the LLM confirms success and the system reveals the reward or next level.
-	If the user exceeds allowed attempts, the LLM denies further guesses and shows a rate-limited lockout message.
-	The session ends.
  
### 2.1.1 Activity Diagram

<img width="100%" height="100%" alt="image" src="https://github.com/user-attachments/assets/0418989c-553f-45c0-a2e4-baa50e7b124c" />

### 2.1.2 Mock-up

<img width="75%" height="75%" alt="image" src="https://github.com/user-attachments/assets/8eaef4fa-74ef-4b5c-88ab-fa7b0f36ae8b" />

### 2.1.3 Narrative

```gherkin
Feature: Interact with Gatekeeper LLM to guess the hidden password

  As a registered player
  I want to chat with the AI gatekeeper
  So that I can outsmart its guardrails and reveal the hidden password

  Background:
    Given I am a signed-in player on the jAilbreak website
    And I have access to the "Game" page
    And the system has initialized a new game session

  Scenario: Start a new challenge
    When I click "Send Message" to begin the chat
    Then the LLM greets me as the Gatekeeper
    And explains that my mission is to discover the hidden password

  Scenario: Attempt to guess the password
    Given the Gatekeeper refuses to reveal the password directly
    When I send creative or indirect prompts to the LLM
    Then the LLM responds according to the current guardrails
    And I receive feedback such as "refused" or a cryptic response

  Scenario: Enter the correct password
    Given I have discovered the hidden password through reasoning or conversation
    When I type the password into the password-check window
    Then the system validates it
    And the LLM announces "Access Granted — you’ve bypassed the guardrails!"
    And the next level becomes unlocked

  Scenario: Submit incorrect password
    Given I have entered an invalid password
    When I submit it in the password-check window
    Then the system displays "Access Denied"
    And I remain on the same challenge level
```

## 2.2 Alternative Flows
(n/a)

# 3 Special Requirements

-	Simulation-only: System must ensure the challenge uses fictional passwords, not production secrets.
- Rate limiting & lockouts: Limit maximum prompt size (e.g., 300 characters).
- Content filtering: LLM must refuse requests for real-world illicit help and log such attempts.
- Configurable difficulty: Each level should be configured with a gurad rails.
- Privacy: Chat transcripts shouldn't be visible to anyone.
- Replayability safety: Ensure the LLM uses deterministic or auditable randomness so challenges can be reproduced for debugging.


# 4 Preconditions
## 4.1 Login
The user has to be logged in to the system.

## 4.2 Server Status 
System should be online 

# 5 Postconditions
(n/a)
 
# 6 Extension Points
(n/a)
