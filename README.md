# AI Travel Packing Assistant

AI Travel Packing Assistant is an information system that uses generative AI to create a personalized travel packing list based on user-provided trip information.

The user provides information such as destination, trip duration, season, trip type, planned activities, luggage type, and additional preferences. The system validates the input, builds a prompt, sends it to the Gemini API, processes the generated response, and returns a structured packing list.

## UMLs

### PlantUML Component diagram

```plantuml
@startuml

actor User

rectangle "AI Travel Packing Assistant" {

    component "User Interface" as UI
    component "Input Validator" as Validator
    component "Prompt Builder" as Prompt
    component "Gemini API Client" as Client
    component "Response Processor" as Response
    component "Packing List Output" as Output
}

cloud "Gemini API" as Gemini

User --> UI : Travel information
UI --> Validator : Raw input
Validator --> Prompt : Validated travel data
Prompt --> Client : Generated prompt

Client --> Gemini : API request
Gemini --> Client : Generated response

Client --> Response : Raw AI response
Response --> Output : Structured packing list
Output --> UI : Formatted result
UI --> User : Personalized packing list

@enduml
```
![Component Diagram](diagrams/images/component.png)
---

### Mermaid UML

```mermaid
flowchart LR

    User([User])

    subgraph System["AI Travel Packing Assistant"]
        UI["User Interface"]
        Validator["Input Validator"]
        Prompt["Prompt Builder"]
        Client["Gemini API Client"]
        Response["Response Processor"]
        Output["Packing List Output"]
    end

    Gemini["Gemini API"]

    User -->|"Travel information"| UI
    UI -->|"Raw input"| Validator
    Validator -->|"Validated travel data"| Prompt
    Prompt -->|"Generated prompt"| Client

    Client -->|"API request"| Gemini
    Gemini -->|"Generated response"| Client

    Client -->|"Raw AI response"| Response
    Response -->|"Structured packing list"| Output
    Output -->|"Formatted result"| UI
    UI -->|"Personalized packing list"| User
```

### PlantUML Sequence diagram

```plantuml
@startuml

actor User

participant "User Interface" as UI
participant "Input Validator" as Validator
participant "Prompt Builder" as Prompt
participant "Gemini API Client" as Client
participant "Gemini API" as Gemini
participant "Response Processor" as Response

User -> UI : Enter travel information
User -> UI : Request packing list

UI -> Validator : Validate input

alt Invalid input
    Validator --> UI : Validation errors
    UI --> User : Display error message

else Valid input
    Validator --> UI : Validated travel data

    UI -> Prompt : Build prompt
    Prompt --> UI : Generated prompt

    UI -> Client : Generate packing list
    Client -> Gemini : Send prompt

    Gemini --> Client : Generated response
    Client --> UI : Raw AI response

    UI -> Response : Process response
    Response --> UI : Structured packing list

    UI --> User : Display personalized packing list
end

@enduml
```

![Sequence Diagram](diagrams/images/sequence.png)

---

### Mermaid UML

```mermaid
sequenceDiagram

    actor User
    participant UI as User Interface
    participant Validator as Input Validator
    participant Prompt as Prompt Builder
    participant Client as Gemini API Client
    participant Gemini as Gemini API
    participant Response as Response Processor

    User->>UI: Enter travel information
    User->>UI: Request packing list

    UI->>Validator: Validate input

    alt Invalid input
        Validator-->>UI: Validation errors
        UI-->>User: Display error message

    else Valid input
        Validator-->>UI: Validated travel data

        UI->>Prompt: Build prompt
        Prompt-->>UI: Generated prompt

        UI->>Client: Generate packing list
        Client->>Gemini: Send prompt

        Gemini-->>Client: Generated response
        Client-->>UI: Raw AI response

        UI->>Response: Process response
        Response-->>UI: Structured packing list

        UI-->>User: Display personalized packing list
    end
```
