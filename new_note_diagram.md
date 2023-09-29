# 0.4: New note diagram
## Image of first HTML response
![first response](./assets/first_response.png)
## Image of second HTML response
![second response](./assets/second_response.png)

## Diagram
Diagram request **base URL is `https://studies.cs.helsinki.fi/exampleapp`**.
```mermaid
---
title: New note
---
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: Client browses to the page and sends a GET request to `/notes`.
    activate Server
    rect rgba(0, 162, 232, 0.3)
    note right of Client: 1.
    Server-->>Client: Server sends a 200 HTML response with text/html to the GET request.
    deactivate Server
    end
    activate Client
    Note over Client: Client renders the HTML.
    deactivate Client
    par
    Client->>Server: Rendring triggers both a GET request for CSS to `/main.css`...
    activate Server
    rect rgba(163, 73, 164, 0.3)
    note right of Client: 2.
    Server-->>Client: Server sends a 200 HTML response with text/css to the GET request.
    end
    and
    Client->>Server: ...and a GET request for JavaScript to `/main.js`.
    rect rgba(163, 73, 164, 0.3)
    note right of Client: 2.
    Server-->>Client: Server sends a 200 HTML response with application/javascript to the GET request.
    deactivate Server
    end
    end
    activate Client
    note over Client: Client renders the CSS and executes the JavaScript code.
    Client->>Server: Client sends a GET request to `/data.json`, triggered by the JavaScript code, to fetch the data JSON.
    deactivate Client
    activate Server
    rect rgba(255, 127, 39, 0.3)
    note right of Client: 3.
    Server-->>Client: Server sends a 200 HTML response with application/json to the GET request.
    deactivate Server
    end
    activate Client
    note over Client: Client JavaScript renders the JSON data.
    note over Client: Client fills the form.
    Client->>Server: Client sends a POST request to `/new_note` with the form data as payload.
    deactivate Client
    activate Server
    rect rgba(237, 28, 36, 0.3)
    note right of Client: 4.
    note over Server: Serves saves the data from the payload.
    Server-->>Client: Server sends a 302 redirect response to the POST request.
    deactivate Server
    end
    Client->>Server: Client sends a GET request to `/notes` based on the redirect response.
    activate Server
    rect rgba(0, 162, 232, 0.3)
    note right of Client: 5.
    Server-->>Client: Server sends a 200 HTML response with text/html to the GET request.
    deactivate Server
    end
    activate Client
    Note over Client: Client again renders the HTML.
    par
    deactivate Client
    Client->>Server: Rendring triggers both a GET request for CSS to `/main.css`...
    activate Server
    rect rgba(163, 73, 164, 0.3)
    note right of Client: 6.
    Server-->>Client: Server sends a 200 HTML response with text/css to the GET request.
    end
    and
    Client->>Server: ...and a GET request for JavaScript to `/main.js`.
    rect rgba(163, 73, 164, 0.3)
    note right of Client: 6.
    Server-->>Client: Server sends a 200 HTML response with application/javascript to the GET request.
    deactivate Server
    end
    end
    activate Client
    note over Client: Client renders the CSS and executes the JavaScript code.
    Client->>Server: Client sends a GET request to `/data.json`, triggered by the JavaScript code, to fetch the notes JSON.
    deactivate Client
    activate Server
    rect rgba(255, 127, 39, 0.3)
    note right of Client: 7.
    Server-->>Client: Server sends a 200 HTML response with application/json to the GET request.
    deactivate Server
    end
    activate Client
    note over Client: Client JavaScript renders the JSON data with form data included.
    deactivate Client
```