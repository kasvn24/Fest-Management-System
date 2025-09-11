## College Festival Management System (DBMS)

An academic Database Management Systems project for managing a college festival: events, participants, registrations, schedules, coordinators, sponsors, and results. This repository contains the database schema, sample data/queries, and documentation to set up and explore the system.

### Repository Contents

- `College Festival Management System.sql`: Main SQL file containing schema (DDL), constraints, and possibly seed/sample data (DML).
- `College Festival Management System.pdf`: Project documentation/report describing requirements, design, and outcomes.
- `Lab-Assignment-2-SQL.pdf`: Related lab brief or assignment specification.

### Key Features

- Events and categories with schedules and venues
- Student participants and team formations
- Registrations and payments (if modeled)
- Event coordinators/volunteers and roles
- Sponsors and sponsorship tiers (if modeled)
- Results/judging and awards
- Data integrity enforced via primary/foreign keys and constraints

---

## Quick Start

You can import the SQL into any relational database that supports standard SQL. The most common workflows are shown below.

### 1) Using MySQL or MariaDB

1. Create a database (optional if the script already creates one):

```sql
CREATE DATABASE college_fest_db;
```

2. Import the schema and data:

```bash
mysql -u <username> -p college_fest_db < "College Festival Management System.sql"
```

3. Verify tables:

```sql
SHOW TABLES;
```

### 2) Using PostgreSQL

1. Create a database:

```bash
createdb college_fest_db
```

2. Import the schema and data:

```bash
psql -U <username> -d college_fest_db -f "College Festival Management System.sql"
```

3. Verify tables:

```sql
\dt
```

> Note: The provided SQL should be largely standard. If you encounter dialect-specific errors, adjust syntax for your RDBMS (e.g., `AUTO_INCREMENT` → `SERIAL` for PostgreSQL, `NOW()` → `CURRENT_TIMESTAMP`, quoted identifiers, etc.).

---

## Example Queries

Below are sample queries you can adapt to your schema. Replace table/column names if they differ.

```sql
-- List all events with their venue and start time
SELECT e.event_id, e.event_name, v.venue_name, e.start_time
FROM events e
JOIN venues v ON v.venue_id = e.venue_id
ORDER BY e.start_time;

-- Find participants registered for a specific event
SELECT p.participant_id, p.full_name, r.team_id
FROM registrations r
JOIN participants p ON p.participant_id = r.participant_id
WHERE r.event_id = 101;

-- Show top 3 teams by points/score for an event
SELECT t.team_id, t.team_name, res.score
FROM results res
JOIN teams t ON t.team_id = res.team_id
WHERE res.event_id = 101
ORDER BY res.score DESC
LIMIT 3;
```

---

## Project Structure

```
College Festival Management System/
├─ README.md
├─ College Festival Management System.sql
├─ College Festival Management System.pdf
└─ Lab-Assignment-2-SQL.pdf
```

---

## How to Use This Project

- Read the PDF(s) to understand the requirements, ER model, and constraints.
- Import the SQL into your RDBMS to create tables and (optionally) load sample data.
- Explore the schema: list tables, inspect constraints, and run example queries.
- Extend with your own queries for analytics, reporting, or administration.

### Common Tasks

- Add a new event:

```sql
INSERT INTO events (event_name, category_id, venue_id, start_time, end_time)
VALUES ('Hackathon', 2, 5, '2025-10-12 09:00:00', '2025-10-12 21:00:00');
```

- Register a participant/team:

```sql
INSERT INTO registrations (event_id, participant_id, team_id, registered_at)
VALUES (101, 20045, NULL, CURRENT_TIMESTAMP);
```

---

## Assumptions and Notes

- The `.sql` file may include both DDL and DML. If it creates a database, you can omit manual `CREATE DATABASE`.
- If foreign key errors appear during import, ensure tables are created in correct order or temporarily disable FK checks (MySQL: `SET FOREIGN_KEY_CHECKS=0;`). Remember to re-enable them.
- Time zones and date formats should be verified based on your RDBMS settings.

---

## Contributing

Contributions are welcome. For significant changes:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-change`
3. Commit with clear messages
4. Open a Pull Request describing the change and rationale

Please include sample data/queries if you introduce new tables or relationships.

---

## License

No license file is currently provided. If you intend this work to be open-source, consider adding a license (e.g., MIT, Apache 2.0). Until a license is added, all rights are reserved by default.

---

## Acknowledgments

- Built as part of a Database Management Systems coursework
- Thanks to mentors, peers, and open educational resources that inspired the schema and queries



