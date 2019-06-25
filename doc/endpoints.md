## Data structure

- Account
  - account_id: int
  - account_name: string
  - account_screen_name: string
  - account_image_url: string
- Chat
  - chat_id: int
  - account: Account
  - messages: List<Message>
  - started_at: ISO 8601 string
  - finished_at ISO 8601 string/null
- Message
  - message_id: int
  - text: string
  - by_anonymous: boolean
- ChatAbstract
  - chat_id: int
  - beginning_message: string
  - started_at: ISO 8601 string
  - finished_at ISO 8601 string/null

## Scenario 0: Everyone

- GET `/account/:account_id`
  - no request parameters
  - response
    - account: Account

- GET `/account/:account_id/chats`
  - only finished chats
  - no request parameters
  - response:
    - chat_abstracts: List<ChatAbstract>

- GET `/account/:account_id/chat/:chat_id`
  - no request parameters
  - response:
    - chat: Chat

## Scenario 1: Account

### Registeration

#### Twitter

- GET `/login`
  - no request parameters
  - response
    - redirect_url: string
      - e.g. `https://api.twitter.com/oauth/authenticate?oauth_token=NPcudxy0yU5T3tBzho7iCotZ3cnetKwcTIRlX0iwRl0`
- GET `/callback`
  - This endpoint is used as callback_url of twitter sign in
  - request
    - oauth_token: string
    - oauth_verifier: string
  - response
    - This endpoint renders Vue.js application in which session token is embedded
      - This Vue.js application saves session token in localStorage

### Chat

#### JSON API

- GET `/me/chats`
  - requires authorization
  - no request parameters
  - response
    - chat_abstracts: List<ChatAbstract>
- GET `/me/chat/:chat_id`
  - requires authorization
  - no request parameters
  - response
    - chat: Chat

#### WebSocket

- GET `/connect/chat/:chat_id`
  - requires authorization

- Send text
  - type: string = "text"
  - text: string
- Finish
  - type: string = "finish"

## Scenario 2: Anonymous

### Chat

#### JSON API

- POST `/anonymous/account/:account_id/chats`
  - request
    - beginning_text: string
  - response
    - chat_id: int
    - session_token: string

#### WebSocket

- GET `/anonymous/connect/chat/:chat_id`
  - WebSocket connection endpoint
  - requires anonymous authentication

- Send text
  - type: string = "text"
  - text: string