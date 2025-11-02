DataEngineering_TWSE_TPEX
Automated Taiwan Stock Market Data Pipeline (TWSE & TPEX)

🧩 Overview
This project builds an automated distributed ETL pipeline for collecting, cleaning, and storing daily stock data from both the Taiwan Stock Exchange (TWSE) and the Taipei Exchange (TPEX).

It uses Apache Airflow (CeleryExecutor) for orchestration, Redis as the message broker and result backend, and Docker Swarm to manage containers across multiple nodes. All cleaned data is stored in MySQL, and task monitoring is provided via Flower.

⚙️ Architecture

🗂 Project Structure
DataEngineering_twse_tpex/
├── airflow.yml
├── docker-compose.yml
├── dataflow/
│   ├── crawler/
│   ├── etl/
│   ├── backend/
│   ├── dags/
│   └── schema/
├── Makefile
└── requirements.txt
🚀 Workflow Summary
1️⃣ Airflow Scheduler triggers daily DAGs. 2️⃣ Tasks are sent to the Redis queue. 3️⃣ Celery Workers execute crawlers. 4️⃣ Fetch TWSE/TPEX data. 5️⃣ Clean, validate, and upload to MySQL. 6️⃣ Flower monitors the workers and queue. 7️⃣ (Optional) FastAPI provides data query endpoints.

🧠 Tech Stack
Category	Tool
Orchestration	Apache Airflow (CeleryExecutor)
Broker / Backend	Redis 5.0
Database	MySQL 8.0
Monitoring	Flower
Language	Python 3.11
Framework	pandas, SQLAlchemy, Pydantic
Container Management	Docker Swarm
🐳 Docker Swarm Deployment Example
docker stack deploy -c airflow.yml airflow
docker service ls
docker service ps airflow_webserver
🪶 Example Access
Component	URL	Description
Airflow UI	http://:8888	DAG monitoring
Flower	http://:5555	Task queue status
MySQL	mysql://:3306	Data storage
