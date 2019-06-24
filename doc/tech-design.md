## Technical design 

### Overview

- Web application
  - Frontend: Vue.js
  - Backend: Go
  - Database: PostgreSQL

### Domain Language

- Account
  - Chat開始の対象となれる人間(StoryのKoji Sakashita)
- Anonymous
  - AccountとChatをする人間(Storyの質問者)
- Chat
  - AccountとAnonymousの間でやりとりされるMessageのSequence
- Message
  - 文章

### ER図

![](./erd.png)