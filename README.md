


## Design DB model for Guvi Zen class
mysql-EER Diagram :

-- Create Database
CREATE DATABASE zen_class;
USE zen_class;

-- Create Users Table
CREATE TABLE users (
    user_id INTEGER AUTO_INCREMENT PRIMARY KEY,
    user_name VARCHAR(255),
    email VARCHAR(255),
    createdAt DATETIME,
    batch INTEGER,
    FOREIGN KEY (batch) REFERENCES batch_data(batch_id)
);

-- Insert Data into Users Table
INSERT INTO users (user_name, email, createdAt, batch) VALUES
('karthik', 'karthi@gmail.com', CURRENT_TIMESTAMP(), 1),
('gayu', 'gayu@gmail.com', CURRENT_TIMESTAMP(), 2),
('maha', 'maha@gmail.com', CURRENT_TIMESTAMP(), 3),
('mugilan', 'mugil@gmail.com', CURRENT_TIMESTAMP(), 4),
('iniya', 'iniya@gmail.com', CURRENT_TIMESTAMP(), 5);

-- Create Batch Data Table
CREATE TABLE batch_data (
    batch_id INT AUTO_INCREMENT PRIMARY KEY,
    batch_name VARCHAR(100)
);

-- Insert Data into Batch Data Table
INSERT INTO batch_data (batch_name) VALUES
('full stack-2023'),
('full stack-2023'),
('html-2023'),
('css-2023'),
('mongodb-2023');

-- Create Codeketa Table
CREATE TABLE codeketa (
    code_id INTEGER AUTO_INCREMENT PRIMARY KEY,
    user_id INTEGER,
    number_of_problem INTEGER,
    status_problem VARCHAR(255),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Insert Data into Codeketa Table
INSERT INTO codeketa (user_id, number_of_problem, status_problem) VALUES
(6, 20, 'pending'),
(6, 20, 'finished'),
(7, 40, 'finished'),
(7, 40, 'finished'),
(8, 50, 'finished');

-- Create Company Drives Table
CREATE TABLE company_drives (
    drive_id INTEGER AUTO_INCREMENT PRIMARY KEY,
    user_id INTEGER,
    drive_date DATE,
    company VARCHAR(100),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Insert Data into Company Drives Table
INSERT INTO company_drives (user_id, drive_date, company) VALUES
(6, makedate(2024, 3), 'Apple'),
(6, makedate(2024, 5), 'Amazon'),
(7, makedate(2024, 3), 'Zomato'),
(7, makedate(2023, 12), 'Flipkart'),
(8, makedate(2023, 5), 'TCS');

-- Create Mentors Table
CREATE TABLE mentors (
    mentorid INTEGER AUTO_INCREMENT PRIMARY KEY,
    mentorname VARCHAR(100),
    mentoremail VARCHAR(100)
);

-- Insert Data into Mentors Table
INSERT INTO mentors (mentorname, mentoremail) VALUES
('Surya', 'suryakumar@gmail.com'),
('Viji', 'vijay@gmail.com'),
('arun', 'arun@gmail.com'),
('prabhu', 'prabhu@gmail.com'),
('naga', 'naga@gmail.com');

-- Create Topics Table
CREATE TABLE topics (
    topicid INTEGER AUTO_INCREMENT PRIMARY KEY,
    topic VARCHAR(200),
    topic_date DATE,
    mentor_id INTEGER,
    FOREIGN KEY (mentor_id) REFERENCES mentors(mentorid)
);

-- Insert Data into Topics Table
INSERT INTO topics (topic, topic_date, mentor_id) VALUES
('HTML - Basics', '2023-04-01', 1),
('NodeJS - Basics', '2023-06-03', 2),
('JavaScript - Basics', '2023-07-05', 3),
('React - Basics', '2023-08-06', 4),
('mysql - Basic', '2023-09-05', 5);

-- Create Tasks Table
CREATE TABLE tasks (
    taskid INTEGER AUTO_INCREMENT PRIMARY KEY,
    topic_id INTEGER,
    task VARCHAR(1000),
    batch_id INTEGER,
    FOREIGN KEY (topic_id) REFERENCES topics(topicid),
    FOREIGN KEY (batch_id) REFERENCES batch_data(batch_id)
);

-- Insert Data into Tasks Table
INSERT INTO tasks (topic_id, task, batch_id) VALUES
(1, 'HTML Task', 1),
(2, 'Javascript Task', 2),
(3, 'React Task', 3),
(4, 'NodeJs Task', 4),
(5, 'Mysql task', 5);

-- Create Attendance Table
CREATE TABLE attendance (
    attendanceid INTEGER AUTO_INCREMENT PRIMARY KEY,
    user_id INTEGER,
    topicsid INTEGER,
    attended BOOLEAN,
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (topicsid) REFERENCES topics(topicid)
);

-- Insert Data into Attendance Table
INSERT INTO attendance (user_id, topicsid, attended) VALUES
(6, 3, true),
(6, 1, true),
(7, 2, false),
(7, 4, true),
(8, 4, true);

-- Example Inner Join
SELECT users.batch, batch_data.batch_id
FROM users
INNER JOIN batch_data ON users.batch = batch_data.batch_id;

