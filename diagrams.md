# Notes App Diagrams – Full Stack Open

These diagrams describe how the browser and server interact in different scenarios of the Notes App from the Full Stack Open course.

---

## 📌 0.4 – New Note Creation (Traditional Multi-Page App)

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note over browser: User writes a note and clicks "Save"

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note over server: Server saves the note to the backend
    server-->>browser: HTTP 302 Redirect to /notes
    deactivate server

    browser->>server: GET /notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET /main.css
    server-->>browser: CSS file

    browser->>server: GET /main.js
    server-->>browser: JavaScript file

    browser->>server: GET /data.json
    server-->>browser: Updated JSON notes

    Note right of browser: JS runs again and renders the updated notes
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET /spa
    activate server
    server-->>browser: HTML document (SPA shell)
    deactivate server

    browser->>server: GET /main.css
    server-->>browser: CSS file

    browser->>server: GET /main.js
    server-->>browser: JavaScript logic for SPA

    Note right of browser: JS dynamically builds the page

    browser->>server: GET /data.json
    server-->>browser: JSON with existing notes

    Note right of browser: JS renders notes into the DOM
sequenceDiagram
    participant browser
    participant server

    Note over browser: User types a note and clicks "Save"

    browser->>server: POST /new_note_spa
    activate server
    Note over server: Server saves the note
    server-->>browser: 201 Created
    deactivate server

    Note right of browser: JS adds the new note directly to the page (no reload)
