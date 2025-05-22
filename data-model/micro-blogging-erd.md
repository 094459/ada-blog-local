# Micro-Blogging Data Model ERD

This Entity Relationship Diagram (ERD) represents the data model for the micro-blogging application.

## Entities

### User
- **id** (PK): Integer, auto-increment
- **email**: String, unique, not null
- **alias**: String, not null
- **bio**: String, nullable
- **created_at**: Datetime, default current timestamp

### Post
- **id** (PK): Integer, auto-increment
- **content**: Text, not null
- **author_id** (FK): Integer, references User.id
- **parent_id** (FK): Integer, references Post.id, nullable
- **responder_id** (FK): Integer, references User.id, nullable
- **created_at**: Datetime, default current timestamp
- **updated_at**: Datetime, default current timestamp, auto-update

### Image
- **id** (PK): Integer, auto-increment
- **post_id** (FK): Integer, references Post.id
- **image_url**: String, not null
- **created_at**: Datetime, default current timestamp

### Link
- **id** (PK): Integer, auto-increment
- **post_id** (FK): Integer, references Post.id
- **url**: String, not null
- **title**: String, nullable
- **created_at**: Datetime, default current timestamp

## Join Tables

### upvotes
- **user_id** (PK, FK): Integer, references User.id
- **post_id** (PK, FK): Integer, references Post.id

### user_follows
- **follower_id** (PK, FK): Integer, references User.id
- **followed_id** (PK, FK): Integer, references User.id
- **created_at**: Datetime, default current timestamp

## Relationships

1. **User to Post (author)**: One-to-many
   - A user can author many posts
   - Each post has one author

2. **User to Post (responder)**: One-to-many
   - A user can respond to many posts
   - Each post response has one responder

3. **Post to Post (parent/responses)**: One-to-many
   - A post can have many responses
   - Each response has one parent post

4. **Post to Image**: One-to-many
   - A post can have many images
   - Each image belongs to one post

5. **Post to Link**: One-to-many
   - A post can have many links
   - Each link belongs to one post

6. **User to Post (upvotes)**: Many-to-many
   - A user can upvote many posts
   - A post can be upvoted by many users
   - Implemented through the upvotes join table

7. **User to User (follows)**: Many-to-many
   - A user can follow many users
   - A user can be followed by many users
   - Implemented through the user_follows join table
