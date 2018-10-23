__MOOCademy__
2 tables

table "courses"
|course_id|title|description|

CREATE TABLE `courses` (
`Course_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`title` TEXT,
`description` TEXT
);

table "lessons"
|lesson_id|course_id|title|body|

CREATE TABLE `lessons` (
`lesson_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`course_id` INTEGER,
`title` TEXT,
`body` TEXT
);


__The Hacking Pinterest__

table "users"
|user_id|name|

CREATE TABLE `users` (
`user_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`name` TEXT
);

table "pins"
|pin_id|user_id|title|URL|

CREATE TABLE `pins` (
`pin_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`user_id` INTEGER,
`title` TEXT,
`URL` TEXT
);

table "comments"
|comment_id|pin_id|user_id|content|

CREATE TABLE `comments` (
`comment_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`pin_id` INTEGER,
`user_id` INTEGER,
`content` TEXT
);


__The Hacking News__

table "users"
|user_id|name|

CREATE TABLE `users` (
`user_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`name` TEXT
);

table "links"
|link_id|user_id|content|

CREATE TABLE `links` (
`link_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`user_id` INTEGER,
`content` TEXT
);

table "comments"
|comment_id|user_id|parent_comment_id|link_id|content|

CREATE TABLE `comments` (
`comment_id` INTEGER PRIMARY KEY AUTOINCREMENT,
`user_id` INTEGER,
`parent_comment_id` INTEGER,
`link_id` INTEGER,
`content` TEXT
);


__The Hacking Class__

table "students"
|student_id|name|course_id|

table "courses"
|course_id|name|
