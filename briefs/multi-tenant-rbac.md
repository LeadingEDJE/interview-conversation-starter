# Brief — multi-tenant RBAC

> **Ade, CTO, mid-size SaaS**
>
> We sell the same product to about two hundred companies and every one of them has their
> own data in our system. The absolute red line is that Company A can never, under any
> circumstances, see Company B's records. That's the thing that ends us if we get it wrong,
> and honestly it's the thing I most want a second opinion on.
>
> Inside a company there are three kinds of people. Owners run the account and can do
> anything. Members do the day-to-day work. Viewers are usually finance or an auditor and
> they just look.
>
> Oh — and our support team needs to be able to pull up a customer's records when someone
> raises a ticket. That happens a dozen times a day and at the moment they ask an engineer,
> which is obviously not sustainable.
>
> Build me the smallest version of this you can that I'd actually trust.

## What it needs to do

Pick any single resource type you like — projects, invoices, notes, whatever. One is
plenty.

1. **Every record belongs to a tenant**, and every request arrives identified with a tenant
   and a role. A header or a stub token is completely fine; you don't need real
   authentication.
2. **The three roles do different things.** Owners can create, read, update and delete.
   Members can create, read and update. Viewers can only read.
3. **No request can reach another tenant's records**, whatever it asks for.

## Not in scope — please don't build these

We mean this. These are the things that turn an hour into an afternoon, and we're not
looking for them:

- Real authentication — no login, no password hashing, no signed tokens, no identity provider
- Endpoints for managing users, roles, or tenants
- Token expiry or refresh
- More than one resource type
- A UI
- Pagination
- A real database, if in-memory or files on disk will do
- Caching, or rate limiting
- Generated API documentation
- Input validation beyond what the permission rules need
- Migrations, CI config, structured logging, or metrics

If you're reaching for one of these, that's the signal to stop.

## Done

When those three things work, and it runs in a container, and you can show it working —
**you are done. Stop.**
