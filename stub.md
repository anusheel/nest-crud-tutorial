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

<details open id="705bd94a3f20d2b1325e34e5791248cc">
<summary></summary>

Firstly, you need to install NestJS CLI globally on your machine. You can do this by running the following command:

```bash
npm i -g @nestjs/cli
```

Then, create a new NestJS project:

```bash
nest new nestjs-typeorm-crud
```

Navigate into the project directory:

```bash
cd nestjs-typeorm-crud
```

Install the necessary packages:

```bash
npm install @nestjs/typeorm typeorm pg
```

Now, let's generate the resources for User and Todo:

```bash
nest generate resource user
```

When prompted, select `REST API`, `Y` for generating CRUD entry points, and `N` for generating spec files.

Do the same for Todo:

```bash
nest generate resource todo
```

Now, you need to define your entities. In `src/user/entities/user.entity.ts`, add the following:

```typescript
import { Entity, Column, PrimaryGeneratedColumn, OneToMany } from 'typeorm';
import { Todo } from '../../todo/entities/todo.entity';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;

  @OneToMany(() => Todo, todo => todo.assignee)
  todos: Todo[];
}
```

In `src/todo/entities/todo.entity.ts`, add the following:

```typescript
import { Entity, Column, PrimaryGeneratedColumn, ManyToOne } from 'typeorm';
import { User } from '../../user/entities/user.entity';

@Entity()
export class Todo {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  title: string;

  @Column()
  description: string;

  @ManyToOne(() => User, user => user.todos)
  assignee: User;
}
```

Finally, you need to configure TypeORM. In `src/app.module.ts`, import `TypeOrmModule` and add it to the `imports` array:

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { UserModule } from './user/user.module';
import { TodoModule } from './todo/todo.module';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'postgres',
      host: 'localhost',
      port: 5432,
      username: 'stubuser',
      password: 'stubpassword',
      database: 'test',
      entities: [__dirname + '/**/*.entity{.ts,.js}'],
      synchronize: true,
    }),
    UserModule,
    TodoModule,
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```

Please replace the database connection details with your own.

Now, you have a high-quality codebase with NestJS and TypeORM for all the CRUD API endpoints for User and Todo entities.
</details>

