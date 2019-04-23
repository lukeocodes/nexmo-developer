Before proceeding any further, here are couple of concepts that you'll need to understand.

* **Nexmo Applications** - These contain configuration for the application that you are building.
* **JWTs** ([JSON Web Tokens](https://jwt.io/)) - the Client SDK API uses JWTs for authentication. JWTs contain all the information the Nexmo platform needs to authenticate requests. JWTs also contain information such as the associated Applications, Users and permissions.
* **Users** - users who are associated with the Nexmo Application. It's expected that Users will have a one-to-one mapping with your own authentication system.
* **Conversations** - A thread of conversation between two or more Users.
* **Members** - Users that are part of a conversation.