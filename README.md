# World Cup Database

## Overview

The **World Cup Database** is a Bash and PostgreSQL project that stores FIFA World Cup match data in a relational database and performs statistical analysis through SQL queries.

The project consists of two main scripts:

* **insert_data.sh** – Imports World Cup data from a CSV file into PostgreSQL.
* **queries.sh** – Executes SQL queries to retrieve tournament statistics and insights.

This project demonstrates database design, data normalization, Bash scripting, and SQL query development.

---

## Features

### Data Import

* Reads World Cup match data from a CSV file
* Automatically inserts teams into the database
* Prevents duplicate team records
* Establishes relationships between teams and matches
* Populates the database using PostgreSQL

### Data Analysis

Generate insights such as:

* Total goals scored by winning teams
* Total goals scored by all teams
* Average goals per game
* Highest-scoring match performances
* Tournament champions
* Teams participating in specific rounds
* Winning team statistics
* Team searches using pattern matching

---

## Technologies Used

* Bash Shell Scripting
* PostgreSQL
* SQL
* CSV Data Processing
* Linux Command Line

---

## Database Schema

### Teams Table

```sql
CREATE TABLE teams (
    team_id SERIAL PRIMARY KEY,
    name VARCHAR(20) UNIQUE NOT NULL
);
```

### Games Table

```sql
CREATE TABLE games (
    game_id SERIAL PRIMARY KEY,
    year INT NOT NULL,
    round VARCHAR(20) NOT NULL,
    winner_id INT REFERENCES teams(team_id),
    opponent_id INT REFERENCES teams(team_id),
    winner_goals INT NOT NULL,
    opponent_goals INT NOT NULL
);
```

### Database Relationship

```text
Teams
│
├── team_id (PK)
└── name

Games
│
├── game_id (PK)
├── year
├── round
├── winner_id (FK → teams.team_id)
├── opponent_id (FK → teams.team_id)
├── winner_goals
└── opponent_goals
```

---

## Project Structure

```text
world-cup-database/
│
├── insert_data.sh
├── queries.sh
├── games.csv
├── worldcup.sql
└── README.md
```

---

## Setup Instructions

### 1. Create the Database

```bash
psql -U freecodecamp < worldcup.sql
```

### 2. Import the Data

```bash
chmod +x insert_data.sh
./insert_data.sh
```

### 3. Run Statistical Queries

```bash
chmod +x queries.sh
./queries.sh
```

---

## Sample Queries

### Total Goals by Winning Teams

```sql
SELECT SUM(winner_goals)
FROM games;
```

### World Cup Champion (2018)

```sql
SELECT t.name
FROM teams t
JOIN games g
ON t.team_id = g.winner_id
WHERE g.year = 2018
AND g.round = 'Final';
```

### Teams Starting with "Co"

```sql
SELECT name
FROM teams
WHERE name LIKE 'Co%';
```

---

## Learning Objectives

This project demonstrates:

* Relational Database Design
* Data Normalization
* Foreign Key Relationships
* SQL Queries
* Aggregate Functions
* JOIN Operations
* CSV Data Importing
* Bash Scripting Automation
* PostgreSQL Database Management

---

## Example Dataset

The database includes FIFA World Cup knockout-stage matches from:

* 2014 FIFA World Cup
* 2018 FIFA World Cup

Sample teams:

* France
* Croatia
* Germany
* Brazil
* Argentina
* Belgium
* England
* Netherlands

---

## Future Improvements

* Support additional World Cup tournaments
* Import data automatically from external sources
* Generate reports and visualizations
* Create a web-based dashboard
* Add player statistics
* Track tournament records over time

---

## Author

Created as part of the FreeCodeCamp Relational Database Certification Project.

**Developer:** Hero Park

---

## License

This project is for educational and learning purposes.
