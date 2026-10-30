# TaskFlow

A small, dependency-light task manager built with Flask. It ships with a clean web UI, a JSON REST API backed by SQLite, and a test suite wired into GitHub Actions.

![CI](https://github.com/your-username/taskflow/actions/workflows/ci.yml/badge.svg)
![Python](https://img.shields.io/badge/python-3.11%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

- Create, update, complete and delete tasks
- Priorities: `low`, `medium`, `high`
- Filter by all / active / done with live stats
- SQLite storage, zero configuration
- Clean REST API with input validation
- Responsive dark UI, no build step
- Tests + CI on Python 3.11, 3.12 and 3.13

## Getting started

```bash
git clone https://github.com/your-username/taskflow.git
cd taskflow

python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
python run.py
```

Open <http://127.0.0.1:5000>. The database is created automatically at `instance/taskflow.sqlite`.

## API

Base URL: `/api`

| Method | Endpoint        | Description        |
| ------ | --------------- | ------------------ |
| GET    | `/health`       | Health check       |
| GET    | `/tasks`        | List all tasks     |
| POST   | `/tasks`        | Create a task      |
| GET    | `/tasks/<id>`   | Get one task       |
| PUT    | `/tasks/<id>`   | Update a task      |
| DELETE | `/tasks/<id>`   | Delete a task      |

### Example

```bash
curl -X POST http://127.0.0.1:5000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Ship the project", "priority": "high"}'
```

```json
{
  "id": 1,
  "title": "Ship the project",
  "description": "",
  "priority": "high",
  "done": false,
  "created_at": "2026-01-01 10:00:00"
}
```

Validation errors return `400` with a message:

```json
{ "error": "priority must be one of: low, medium, high" }
```

## Tests

```bash
python -m unittest discover -s tests -v
# or, with the dev dependencies installed
pytest -q
```

## Project layout

```
taskflow/
├── app/
│   ├── __init__.py      # application factory
│   ├── db.py            # SQLite helpers
│   ├── routes.py        # web + API routes
│   ├── templates/       # Jinja templates
│   └── static/          # CSS and JS
├── tests/
│   └── test_app.py
├── run.py
└── requirements.txt
```

## License

[MIT](LICENSE)
