# Brief — document store

> **Priya, engineering manager, internal platform team**
>
> Four teams here are each storing blobs of JSON somewhere different — one's got a Mongo
> instance nobody maintains, one's writing files to a share, two are using columns in
> Postgres. The shapes are all different and they change constantly, so we don't want to
> impose a schema on them.
>
> What I want is one boring service they can all POST a document to and get it back later.
> The part that keeps coming up is history: when something looks wrong, people need to see
> what the document looked like before it was changed. Right now nobody can answer that and
> it turns into an afternoon of grep.
>
> I don't need it to be clever. I need it to be obvious.

## What it needs to do

1. **Save a JSON document** under a collection name and an id. Any shape — you don't know
   what's in it, and you shouldn't need to.
2. **Fetch it back** by collection and id, and **list** what's in a collection.
3. **Keep the previous content when a document is updated**, and make it retrievable.

## Not in scope — please don't build these

We mean this. These are the things that turn an hour into an afternoon, and we're not
looking for them:

- Authentication or authorisation of any kind
- Pagination
- Delete
- Search, filtering, or any kind of query language
- A UI
- A real database, if in-memory or files on disk will do
- Validating the shape of documents
- Caching, or rate limiting
- Generated API documentation
- Migrations, CI config, structured logging, or metrics

If you're reaching for one of these, that's the signal to stop.

## Done

When those three things work, and it runs in a container, and you can show it working —
**you are done. Stop.**
