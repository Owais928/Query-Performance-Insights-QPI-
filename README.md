# Query Performance Insights (QPI)
A Professional Oracle APEX 24.2 Region Plugin for SQL Performance Monitoring

---

## Overview

Query Performance Insights (QPI) is an Oracle APEX 24.2 region plug-in that provides real-time SQL execution monitoring directly inside APEX applications.

It enables developers and architects to measure execution time, analyze execution plans, detect plan changes, and track performance trends without leaving the application interface.

---

## Features

- Real-time execution time measurement (milliseconds)
- Row count tracking
- SQL_ID detection
- Plan Hash Value detection
- Execution Plan Viewer (DBMS_XPLAN)
- Plan change detection
- Historical run logging
- Configurable warning and error thresholds
- Professional modal UI with copy support
- Enterprise-safe architecture

---

## Requirements

- Oracle APEX 24.2
- Oracle Database 19c / 21c / 23c / 26ai
- Required grants:

```sql
GRANT SELECT ON V_$SQL TO <SCHEMA>;
GRANT SELECT ON V_$SQL_PLAN TO <SCHEMA>;
GRANT SELECT ON V_$SQL_PLAN_STATISTICS_ALL TO <SCHEMA>;
```

---

## Installation

1. Import the plug-in SQL file in:
   Shared Components → Plug-ins → Import

2. Upload plugin static files:
   - qpi.js
   - qpi.css

3. Create the performance log table:

```sql
create table qpi_run_log (
  id number generated always as identity primary key,
  app_id number,
  page_id number,
  region_static_id varchar2(200),
  query_hash varchar2(64),
  run_ts timestamp default systimestamp,
  elapsed_ms number,
  rows_returned number,
  plan_hash number,
  sql_id varchar2(13),
  child_number number,
  plan_text clob
);
```

---

## Plugin Attributes

| Attribute | Description |
|------------|------------|
| SQL Query | Query to execute and measure |
| Sample Rows | Maximum rows to sample |
| Warn Time (ms) | Warning threshold |
| Error Time (ms) | Error threshold |
| Enable Plan Check | Enable DBMS_XPLAN capture |
| Save History | Store execution in log table |

---

## How It Works

1. Query executed via DBMS_SQL
2. Unique marker comment ensures reliable SQL_ID detection
3. Execution plan retrieved via DBMS_XPLAN.DISPLAY_CURSOR
4. Plan safely aggregated using XMLAGG (CLOB-safe)
5. JSON returned via APEX_JSON
6. Frontend renders performance card and plan viewer

---

## UI Highlights

- Clean card layout
- Status badge (Good / Warning / Issue)
- Execution trend comparison
- Plan change warning
- Professional modal execution plan viewer
- Copy-to-clipboard support

---

## Security Considerations

- Only SELECT statements allowed
- No DML execution
- No dynamic privilege escalation
- Graceful fallback when V$ privileges unavailable

---

## Roadmap

- Performance trend charts
- Plan diff comparison
- Full scan highlighting
- AI-assisted optimization suggestions
- Export plan functionality

---

## License

MIT License

---

## Author

MUHAMMAD AWAIS  
Oracle APEX Developer  
https://oratechbyawais.blogspot.com/

---

Performance should be visible.  
QPI makes it measurable.
