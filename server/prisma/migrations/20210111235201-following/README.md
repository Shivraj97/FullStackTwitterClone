# Migration `20210111235201-following`

This migration has been generated by Nik at 1/11/2021, 3:52:01 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "public"."Following" (
"id" SERIAL,
"name" text   NOT NULL ,
"avatar" text   NOT NULL ,
"followId" integer   NOT NULL ,
"userId" integer   ,
PRIMARY KEY ("id")
)

ALTER TABLE "public"."Following" ADD FOREIGN KEY("userId")REFERENCES "public"."User"("id") ON DELETE SET NULL ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20210109004635-comment-reply..20210111235201-following
--- datamodel.dml
+++ datamodel.dml
@@ -3,9 +3,9 @@
 }
 datasource postgresql {
   provider = "postgresql"
-  url = "***"
+  url = "***"
 }
 model Tweet {
   id        Int          @id @default(autoincrement())
@@ -25,8 +25,9 @@
   tweets     Tweet[]
   Profile    Profile?
   likedTweet LikedTweet[]
   comments   Comment[]
+  Following  Following[]
 }
 model LikedTweet {
   id      Int      @id @default(autoincrement())
@@ -36,8 +37,17 @@
   User    User?    @relation(fields: [userId], references: [id])
   tweetId Int
 }
+model Following {
+  id       Int    @id @default(autoincrement())
+  name     String
+  avatar   String
+  followId Int
+  User     User?  @relation(fields: [userId], references: [id])
+  userId   Int?
+}
+
 model Profile {
   id        Int      @id @default(autoincrement())
   createdAt DateTime @default(now())
   bio       String?
```


