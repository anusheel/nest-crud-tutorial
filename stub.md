---
system_prompt: For any parts of your response that include code, make sure to include the filename along with the backtick and the code snippets. For any environment variables, use stubuser and stubpassword as the login. For any commands, auto confirm any prompts on stdin. 
model: gpt-4
temperature: 0
---



### Create your prompts below and Stub will generate the code and documentation


```stub
Create a high quality codebase with NestJS and TypeORM for all the CRUD API endpoints with the following 2 entities:
- User, with attributes : name, email
- Todo, with attributes : title, description, assignee
Assignee attribute in Todo is of type User, with each todo having a unique optional user as the assignee.

Use nest generate resource command
```

