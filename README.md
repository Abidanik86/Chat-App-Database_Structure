# Messaging App Database

## Overview
This is the database schema for a WhatsApp-like messaging application. It includes all necessary tables and relationships to manage users, messages, groups, calls, reactions, notifications, and more.

---

## 📂 Database Structure

### 1️⃣ **Users Table (`users`)**
Stores user information.
- **Columns**: `user_id`, `username`, `email`, `phone`, `password`, `status`, `profile_pic`, `created_at`
- **Relationships**: Connected to `contacts`, `messages`, `groups`, `chat_settings`, etc.

### 2️⃣ **Contacts Table (`contacts`)**
Stores user contacts.
- **Columns**: `contact_id`, `user_id`, `contact_user_id`, `created_at`
- **Relationships**: `user_id` and `contact_user_id` reference `users`.

### 3️⃣ **Messages Table (`messages`)**
Stores user messages (one-to-one & group).
- **Columns**: `message_id`, `sender_id`, `receiver_id`, `group_id`, `message_text`, `message_type`, `media_url`, `is_read`, `created_at`
- **Relationships**: `sender_id` and `receiver_id` reference `users`; `group_id` references `groups`.

### 4️⃣ **Groups Table (`groups`)**
Stores group details.
- **Columns**: `group_id`, `group_name`, `admin_id`, `created_at`
- **Relationships**: `admin_id` references `users`.

### 5️⃣ **Group Members Table (`group_members`)**
Stores group participants.
- **Columns**: `member_id`, `group_id`, `user_id`, `role`, `joined_at`
- **Relationships**: `group_id` references `groups`; `user_id` references `users`.

### 6️⃣ **Chat Settings Table (`chat_settings`)**
Manages chat preferences like mute and archive.
- **Columns**: `setting_id`, `user_id`, `chat_type`, `chat_id`, `muted`, `archived`

### 7️⃣ **Secret Chats Table (`secret_chats`)**
Stores encrypted one-on-one secret chats.
- **Columns**: `chat_id`, `user_one`, `user_two`, `encryption_key`

### 8️⃣ **Blocked Users Table (`blocked_users`)**
Stores blocked contacts.
- **Columns**: `block_id`, `user_id`, `blocked_user_id`, `blocked_at`

### 🔹 **Additional Tables (Optional Features)**
These tables extend the app’s functionality.

| Feature        | Table Name           | Description |
|---------------|----------------------|-------------|
| **Reactions** | `message_reactions` | Store reactions (like 👍❤️😂) to messages |
| **Read Receipts** | `message_read_receipts` | Track message delivery & read status |
| **Calls** | `calls` | Store call logs (audio/video) |
| **Call Participants** | `call_participants` | Store participants in group calls |
| **Notifications** | `notifications` | Manage push notifications for messages, calls, etc. |
| **Group Invites** | `group_invites` | Store pending group invitations |
| **Status Updates** | `status_updates` | Store user stories (text, image, video) |
| **Status Views** | `status_views` | Track who viewed a status update |
| **Reports** | `reports` | Allow users to report messages, groups, or users |

---