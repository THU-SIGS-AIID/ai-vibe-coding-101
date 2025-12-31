# Chapter 5: From Database to Supabase

In the previous chapters, we have already touched upon how to use AI for Vibe Coding to quickly build front-end applications and integrate large language models. However, for a truly "complete" application, front-end and AI are often not enough. We also need to consider:

*   **How to store user information?** (Registration, login, personal settings)
*   **How to manage complex data?** (Orders, product lists, chat history)
*   **How to handle files?** (Uploading avatars, sharing images)
*   **How to perform real-time interactions?** (Real-time chat, collaborative editing)

In traditional development, these requirements usually mean you need to build a complex backend system, manage databases, and handle server deployment. For individual developers or AI-assisted development, this is often a huge burden.

This is where **Supabase** comes in. It is an open-source "Backend-as-a-Service" (BaaS) platform that provides almost all the backend capabilities you need (Database, Auth, Storage, Edge Functions, Realtime) in an "out-of-the-box" way, allowing you to focus on the core business logic of your application without worrying about complex infrastructure.

In this chapter, we will take a "Burger Shop" as an example to deeply understand how to use Supabase to add "superpowers" to your application.

## 5.1 Database Basics

Before diving into Supabase, we need to understand the core of almost all applications: the **Database**.

Simply put, a database is a specialized "warehouse" for storing and managing data. Unlike saving data in simple text files or Excel, databases provide more efficient, secure, and reliable ways to organize and query data.

### 5.1.1 Relational vs. Non-Relational Databases

Currently, the two most common types of databases in the industry are:

1.  **Relational Databases (SQL):**
    *   **Data Structure:** Data is organized in "tables," with fixed columns (Fields) and rows (Records).
    *   **Features:** Strong consistency, supports complex queries (JOIN), suitable for data with clear structures (e.g., banking systems, e-commerce orders).
    *   **Examples:** **PostgreSQL** (what Supabase uses), MySQL, SQLite.
2.  **Non-Relational Databases (NoSQL):**
    *   **Data Structure:** Often stored as "Documents" (like JSON), with flexible structures.
    *   **Features:** Easy to scale, high performance, suitable for data with fast-changing or irregular structures (e.g., social media feeds, real-time logs).
    *   **Examples:** MongoDB, Redis.

**Supabase is built on PostgreSQL**, which is one of the most powerful and popular open-source relational databases in the world.

### 5.1.2 How to Represent Data?

How do we represent data in a program? Let's look at three common formats:

#### 1. Programming Language Variables (e.g., Python)
Used for temporary storage while the program is running.
```python
age = 30
is_active = True
scores = [85, 92, 78, 90]
user_info = {
    "age": 30,
    "height": 1.80,
    "login_count": 156
}
```

#### 2. JSON (JavaScript Object Notation)
The standard format for data exchange between front-end and back-end.
```json
{
  "order_id": 901,
  "user_id": 1001,
  "amount": 29.99,
  "status": "completed",
  "items": [
    { "sku": "BG-001", "name": "Beef Burger", "quantity": 1, "price": 18.00 },
    { "sku": "SD-003", "name": "French Fries", "quantity": 1, "price": 6.99 },
    { "sku": "DK-002", "name": "Cola", "quantity": 1, "price": 5.00 }
  ],
  "shipping_address": {
    "street": "123 Tech Park Road",
    "city": "Shenzhen",
    "zip_code": "518057"
  }
}
```

#### 3. SQL (Structured Query Language)
The standard language for communicating with relational databases.
```sql
SELECT
    p.title,
    p.content,
    u.username AS author,
    c.body AS comment,
    t.tag_name AS tag
FROM
    posts p
JOIN
    users u ON p.author_id = u.user_id
LEFT JOIN
    comments c ON p.post_id = c.post_id
LEFT JOIN
    post_tags pt ON p.post_id = pt.post_id
LEFT JOIN
    tags t ON pt.tag_id = t.tag_id
WHERE
    p.post_id = 1;
```

### 5.1.3 Core Concepts of PostgreSQL

*   **Tables:** Where data is actually stored (e.g., `users` table, `orders` table).
*   **Columns (Fields):** Define the type of data (e.g., `username` is Text, `price` is Numeric).
*   **Rows (Records):** Specific data entries.
*   **Primary Key (PK):** A unique identifier for each row (e.g., `user_id`).
*   **Foreign Key (FK):** Used to establish relationships between tables (e.g., the `user_id` in the `orders` table refers to the `user_id` in the `users` table).

### 5.1.4 Row Level Security (RLS)

In traditional development, the backend server controls who can access what data. In Supabase, because the front-end can directly interact with the database, we use **RLS (Row Level Security)** to ensure data security.

RLS allows you to define fine-grained access policies. For example:
*   Users can only read their own profile information.
*   Only administrators can delete orders.
*   Everyone can view public product lists.

This is a core security mechanism in Supabase, and we will configure it in the following sections.

---

## 5.2 Supabase Auth

User authentication is a core part of almost every modern application. Supabase Auth provides a complete set of solutions, including email/password login, social login (Google, GitHub), and magic links.

In the demo project `Project5-Supabase-Demos/apps/project-burger-shop-auth-simple-supabase-1`, we demonstrate the simplest email/password registration and login flow.

![](images/image46.png)

### 5.2.1 Core Process: Email & Password Login

1.  **Registration (`signUp`):** User submits email and password. Supabase creates a user record and sends a verification email (optional).
2.  **Login (`signInWithPassword`):** User submits credentials. Supabase verifies them and returns a **JWT (JSON Web Token)**.
3.  **Session Management:** The Supabase client automatically stores the JWT in the browser (usually in LocalStorage) and includes it in subsequent requests to identify the user.
4.  **Logout (`signOut`):** Clears the local JWT and terminates the session.

### 5.2.2 Setting up Social Login (OAuth)

Social login (like Google or GitHub) provides a much better user experience. To implement this, you need to:
1.  Register an application on the provider's platform (e.g., Google Cloud Console or GitHub Developer Settings).
2.  Get the **Client ID** and **Client Secret**.
3.  Configure these credentials in the Supabase Dashboard.

#### Example: Configuring GitHub Login

1.  **Go to GitHub Developer Settings:**
    1.  Log in to your GitHub account.
    2.  Click your avatar -> "Settings".
    3.  At the bottom of the left sidebar, find "Developer settings".
2.  **Register a new application:**
    1.  Select "OAuth Apps" and click "New OAuth App".
    2.  Fill in the application name, e.g., "My Burger Shop".
    3.  **Homepage URL:** Your app's URL or `http://localhost:3000` for local development.
    4.  **Authorization callback URL:** Your Supabase project's callback URL. You can find this in Supabase Dashboard under "Authentication" -> "Providers" -> "GitHub". It looks like `https://<project-id>.supabase.co/auth/v1/callback`.
3.  **Get Client ID and Client Secret:**
    1.  After registering, you will see your **Client ID**.
    2.  Click "Generate a new client secret" and **copy it immediately**.

### 5.2.4 Configuring Providers in Supabase

1.  Go to Supabase Dashboard.
2.  Select your project -> "Authentication" -> "Providers".
3.  Find "GitHub" and enable it.
4.  Paste the **Client ID** and **Client Secret**.
5.  Click "Save".

Now you can allow users to log in with GitHub! You can refer to `Project5-Supabase-Demos/apps/project-burger-shop-auth-advanced-supabase-6` for a complete implementation.

### 5.2.6 Password Reset Implementation

Password reset is another critical feature. The project `project-burger-shop-auth-advanced-supabase-6` includes a full implementation:

1.  **Request:** User enters email on the "Forgot Password" page. Front-end calls `supabase.auth.resetPasswordForEmail()`.
2.  **Email:** Supabase sends an email with a unique reset link.
3.  **Link:** User clicks the link and is redirected to a reset page in your app.
4.  **Update:** User enters a new password. Front-end calls `supabase.auth.updateUser()`.

You can also customize the email templates in Supabase Dashboard under Authentication -> Email Templates.

---

## 5.3 Realtime Function

Supabase's Realtime capability is one of its most powerful features, making it easy to build collaborative apps, live dashboards, or chat systems.

The project `Project5-Supabase-Demos/apps/project-burger-shop-realtime-orders-3` demonstrates three core Realtime capabilities: **Postgres Changes**, **Broadcast**, and **Presence**.

![](images/image54.png)

### 5.3.1 Postgres Changes

This allows clients to listen to changes in specific database tables, rows, or columns. Once the database changes, Supabase pushes the new data to all subscribed clients via WebSockets.

To enable this, you usually need to run a SQL script:
```sql
-- Enable realtime replication
ALTER TABLE public.chat_messages REPLICA IDENTITY FULL;
DO $$
BEGIN
  IF NOT EXISTS (
    SELECT 1 FROM pg_publication_tables
    WHERE pubname = 'supabase_realtime'
      AND schemaname = 'public'
      AND tablename = 'chat_messages'
  ) THEN
    ALTER PUBLICATION supabase_realtime ADD TABLE public.chat_messages;
  END IF;
END $$;
```

Then, you can listen for changes in your code:
```typescript
const sub = supabase
  .channel('chat_messages_channel')
  .on('postgres_changes', {
    event: 'INSERT',
    schema: 'public',
    table: 'chat_messages'
  }, (payload: any) => {
    console.log('New message received:', payload.new);
    // Update your UI here
  })
  .subscribe();
```

### 5.3.2 Broadcast & Presence

For interactions that don't need to be stored in the database (like cursor positions or "who's online"), use Broadcast and Presence.

*   **Presence:** Tracks shared state among clients (e.g., "User A is online").
*   **Broadcast:** Sends low-latency messages directly between clients (e.g., "Cursor moved to X, Y").

#### Presence Example:
```typescript
const ch = supabase.channel('lobby_presence', {
  config: { presence: { key: userId } }
});

ch.on('presence', { event: 'sync' }, () => {
  const state = ch.presenceState();
  // Update online user list
}).subscribe(async (status) => {
  if (status === 'SUBSCRIBED') {
    await ch.track({ name: 'User Name', color: 'blue' });
  }
});
```

#### Broadcast Example (Cursor Tracking):
```typescript
// Sending
channel.send({
  type: 'broadcast',
  event: 'cursor',
  payload: { x, y, id }
});

// Receiving
channel.on('broadcast', { event: 'cursor' }, ({ payload }) => {
  // Update cursor position on screen
});
```

---

## 5.4 Storage

Applications often need to handle unstructured files like avatars, product images, or documents. Storing these directly in a database is inefficient. Instead, we use **Object Storage**.

In Supabase, files are organized into **Buckets**. Each file gets a unique URL for access.

![](images/image55.png)

### 5.4.1 Buckets and Policies

You can create a Bucket (e.g., `avatars`) and define RLS policies to control who can upload or read files.

```sql
CREATE POLICY "Allow public read access to avatars"
ON storage.objects FOR SELECT
USING ( bucket_id = 'avatars' );
```

### 5.4.2 Getting File URLs

Supabase provides two ways to get a file URL:

1.  **Public URL:** Permanent and easy to cache, but susceptible to "hotlinking" (others stealing your bandwidth).
    ```typescript
    const { data } = supabase.storage.from('avatars').getPublicUrl('path/to/image.png');
    ```
2.  **Signed URL:** Temporary and secure. The link expires after a set time. This is the recommended practice for sensitive or user-specific files.
    ```typescript
    const { data } = await supabase.storage.from('avatars').createSignedUrl('path/to/file.pdf', 3600);
    ```

The project `project-burger-shop-storage-uploads-4` demonstrates a complete avatar upload flow using the `Uppy` library for a great UI and resumable uploads.

---

## 5.5 Edge Functions

**Edge Functions** are server-side TypeScript functions that run on global edge nodes, close to your users. They are perfect for logic that shouldn't happen on the client, such as:
*   Calling third-party APIs with secret keys (e.g., OpenAI).
*   Performing heavy computations (e.g., image processing).
*   Enforcing complex business rules.

Supabase Edge Functions are based on **Deno**.

![](images/image57.png)

### 5.5.1 LLM Chat Example

Suppose you want to call OpenAI's API. You cannot put your API Key in the front-end code. Instead, you create an Edge Function:

```typescript
// supabase/functions/llm-chat/index.ts
import { OpenAI } from "npm:openai";

const OPENAI_API_KEY = Deno.env.get("OPENAI_API_KEY");

Deno.serve(async (req) => {
  const openai = new OpenAI({ apiKey: OPENAI_API_KEY });
  const { prompt } = await req.json();

  const stream = await openai.chat.completions.create({
    model: "gpt-3.5-turbo",
    messages: [{ role: "user", content: prompt }],
    stream: true,
  });

  return new Response(stream.toReadableStream(), {
    headers: { "Content-Type": "text/event-stream" },
  });
});
```

### 5.5.2 Deployment

You can deploy functions directly from the Supabase Dashboard "Edge Functions" panel. Remember to set your **Secrets** (environment variables) like `OPENAI_API_KEY` in the Dashboard.

Other examples in the project include:
*   `txt2img.ts`: Calling image generation APIs.
*   `send-email.ts`: Integrating email services like Resend or SendGrid.

---

## 5.6 Clerk Login

While Supabase has its own Auth, **Clerk** is a specialized tool focused entirely on identity and user management. It offers a more polished UI and advanced features out of the box.

The project `project-burger-shop-auth-advanced-clerk-7` shows how to integrate Clerk with Supabase.

![](images/image61.png)

### 5.6.1 Integration Highlights

1.  **Native Integration:** Supabase and Clerk have an official integration that allows Supabase to verify Clerk's JWTs.
2.  **Data Sync via Webhooks:** When a user registers in Clerk, a Webhook triggers a Supabase Edge Function to sync that user's data into your Supabase `public.users` table.

```typescript
// Example sync logic in Edge Function
case 'user.created': {
  const { id, first_name, last_name, image_url, email_addresses } = evt.data;
  await supabaseAdmin.from('users').insert({
    id, first_name, last_name, image_url,
    email: email_addresses[0]?.email_address,
  });
  break;
}
```

### 5.6.4 Social Login in Clerk

Clerk makes social login very easy. It differentiates between **Development** and **Production** environments:
*   **Development:** Uses shared credentials for quick testing (e.g., `localhost:3000`).
*   **Production:** Requires you to configure your own OAuth credentials from Google/GitHub for security and branding.

---

## 6. From Supabase to More Backend Components (Advanced)

Supabase is a fantastic all-in-one platform, but as your project grows, you might want to explore specialized alternatives for each component.

### Comparison of BaaS Platforms

| Platform | Type | Best For |
| :--- | :--- | :--- |
| **Supabase** | Open-source SQL | Projects needing strong relational data and SQL. |
| **Firebase** | Google Managed | Mobile-first apps, very mature ecosystem. |
| **Appwrite** | Open-source | Developer-friendly, unified API. |
| **Convex** | Frontend-first | Extremely fast iteration, no schema needed. |

### Specialized Alternatives

*   **Auth:** Auth0, Clerk, Logto, Keycloak.
*   **Storage:** Amazon S3, Google Cloud Storage, Cloudinary (for media).
*   **Edge Functions:** Cloudflare Workers, Vercel Edge Functions, AWS Lambda.
*   **Database:** Neon (Serverless Postgres), MongoDB Atlas (NoSQL), CockroachDB (Distributed SQL).

---

## Summary

Today we covered the fundamentals of databases and how Supabase provides a comprehensive backend solution for modern applications. Remember the principle: **Done is better than perfect!** Start with simple features and iterate.

## 📚 Homework

1.  Develop an application that includes a user management system and a database. Try to incorporate more Supabase features like Realtime, Storage, or Edge Functions.
