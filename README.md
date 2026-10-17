🛡️ Indian Army – Predictive Logistics & Forward Supply Chain

Problem Statement ID: 26251 (Software)
Domain: Artificial Intelligence, Machine Learning, GIS & Inventory Management
Project Type: Decision-Support Web Application

Predictive Logistics & Forward Supply Chain is an AI/ML-powered web application designed to improve inventory management, demand forecasting, shortage detection, weather risk assessment, and supply chain visibility through a centralized decision-support dashboard.

[!IMPORTANT]
Disclaimer: This project uses 100% fictional and synthetic data for educational, demonstration, and software development purposes. All locations, coordinates, supply centres, routes, inventory records, and operational scenarios are fictional. No real military deployment locations, operational routes, or confidential information are included.

📑 Table of Contents

Project Overview

Objectives

Key Features

System Modules

Machine Learning Pipeline

GIS and Route Planning

Weather Risk Analysis

Technology Stack

System Architecture

Database Schema

API Documentation

Project Structure

Prerequisites

Installation and Setup

Environment Configuration

Running the Application

Machine Learning Model Training

Security

Future Enhancements

Troubleshooting

References

License

📖 Project Overview

Managing inventory and supply chains in remote and high-altitude environments presents challenges related to uncertain demand, transportation delays, weather conditions, and unexpected shortages.

Traditional inventory management systems often respond to shortages after they occur. This project introduces a predictive, data-driven approach that estimates future demand, identifies potential stock shortages, and provides recommendations for inventory replenishment.

The application combines machine learning, geospatial visualization, weather analysis, and inventory management in a single web-based platform.

Problem Statement

How can AI/ML, GIS, and inventory management technologies be combined to forecast future supply requirements, identify potential shortages, assess transportation delays, and support informed logistics decisions?

Proposed Solution

The system provides a centralized dashboard that enables authorized users to:

Monitor inventory levels across fictional supply centres.

Forecast future consumption using machine learning.

Identify low-stock and at-risk inventory items.

Calculate days of stock coverage and suggested reorder quantities.

Assess weather-related transportation delay risks.

Visualize fictional supply centres and road routes on interactive maps.

Track deliveries and maintain inventory transaction records.

Manage access through role-based authentication.

🎯 Project Objectives

Develop an intelligent inventory management platform.

Forecast future demand using a Random Forest regression model.

Identify potential shortages before inventory reaches critical levels.

Calculate recommended replenishment quantities using demand, lead time, and safety stock.

Visualize fictional supply networks through GIS-based maps.

Analyze weather conditions and estimate potential transportation delays.

Track deliveries and maintain an auditable transaction history.

Provide secure access to dashboards and management features.

Evaluate forecasting performance using MAE and RMSE.

Demonstrate an end-to-end AI-powered decision-support workflow using synthetic data.

🚀 Key Features

FeatureDescriptionAuthenticationJWT-based login and API authenticationRole-Based AccessADMIN, COMMANDER, OPERATOR, and VIEWER rolesCommand DashboardInventory KPIs, risk summaries, and recent activitiesInventory ManagementCreate, view, update, and manage supply item recordsStock TransactionsRecord stock-in and stock-out operationsDemand ForecastingPredict demand for the next 7 or 30 daysShortage DetectionIdentify inventory items at risk of running outReplenishment EngineCalculate suggested reorder quantitiesWeather AnalysisAssess simulated or API-based weather risksGIS MappingDisplay fictional centres using interactive mapsRoute VisualizationDisplay primary and alternative route geometriesDelivery TrackingMonitor delivery status and progressModel EvaluationDisplay forecasting MAE and RMSE metricsAudit HistoryMaintain records of stock transactions

🧩 System Modules

1. Authentication and Access Management

The system uses JSON Web Tokens (JWT) to authenticate users and protect API endpoints.

Supported roles:

RolePermissionsADMINFull system access, including user managementCOMMANDERView reports, monitor risks, and approve supported workflowsOPERATORManage inventory, record stock movements, and update deliveriesVIEWERRead-only access to dashboards and reports

Authorization rules are enforced by the backend rather than relying solely on frontend visibility.

2. Command Dashboard

The dashboard presents a consolidated overview of the application's current state.

Key indicators:

Total inventory records.

Low-stock inventory items.

At-risk fictional supply centres.

Pending and delayed deliveries.

Inventory distribution by category.

Recent inventory and delivery activities.

Active forecasting model and evaluation metrics.

Visualizations:

Pie charts for inventory risk distribution.

Bar charts for inventory categories.

Timeline views for recent activities.

Inventory health indicators based on safety-stock thresholds.

3. Inventory Management

The inventory module manages supply item records and stock balances across fictional supply centres.

Supported operations:

Create and update supply items.

View inventory balances.

Record stock-in and stock-out transactions.

Configure safety-stock thresholds.

View stock health and shortage indicators.

Maintain transaction history.

Inventory validation:

Stock-out operations must not produce negative inventory.

Each accepted transaction should be recorded in the stock ledger.

Inventory updates and corresponding transaction records should be handled atomically.

Unauthorized users must not perform restricted operations.

4. AI/ML Demand Forecasting

The forecasting module uses a RandomForestRegressor to predict future daily consumption.

Forecast horizons:

7-day demand forecast.

30-day demand forecast.

Model features:

day_of_week

month

lag_1

lag_7

lag_14

roll_mean_7

roll_mean_14

The model is trained on synthetic historical consumption data. A chronological train/test split is used to evaluate performance on later observations.

Forecast results can be displayed with prediction values and an uncertainty estimate based on historical model errors.

Note: An RMSE-based interval is an approximate uncertainty band, not automatically a statistically calibrated confidence interval.

5. Shortage Alerts and Replenishment

The shortage analysis module estimates inventory risk using current stock, demand, safety stock, and replenishment lead time.

Days of Cover:

Days of Cover=Current StockAverage Daily Demand\text{Days of Cover} = \frac{\text{Current Stock}}{\text{Average Daily Demand}}

When average daily demand is zero, the application should handle the calculation separately to avoid division-by-zero errors.

Risk categories:

Risk LevelIllustrative Risk ScoreLOW0–24MEDIUM25–44HIGH45–69CRITICAL70–100

The shortage engine can suggest reorder quantities using the following general formula:

Q=max⁡(0,D×L+S−I)Q = \max(0, D \times L + S - I)

Where:

QQ = Suggested reorder quantity.

DD = Forecast average daily demand.

LL = Replenishment lead time in days.

SS = Safety-stock quantity.

II = Current usable inventory.

The final implementation should also account for outstanding orders, incoming deliveries, and any applicable inventory policies.

6. Weather and Delay Risk Analysis

The weather module retrieves weather information from OpenWeatherMap when configured. An offline simulated fallback supports demonstrations without an API key.

Weather factors:

Rainfall and precipitation.

Snow conditions, when available.

Wind speed.

Visibility.

Temperature extremes.

The module produces a delay-risk score between 0 and 100 and maps it to the configured risk categories.

Example recommendations include:

Monitor weather conditions.

Review estimated delivery delays.

Reassess delivery schedules.

Consider postponing a demonstration dispatch when simulated conditions indicate elevated risk.

All weather-based recommendations are decision-support suggestions and should not be treated as guarantees of actual travel conditions.

7. GIS Mapping and Route Visualization

The mapping module visualizes fictional supply centres and transportation connections.

Map layers:

OpenStreetMap street layer.

Esri satellite imagery.

OpenTopoMap terrain layer.

Routing components:

Fictional source and destination selection.

Route geometry retrieval through the OSRM public demonstration service.

Primary and alternative route visualization.

Dynamic addition and removal of fictional map points.

Geospatial distance calculations using the Haversine formula.

Dijkstra's algorithm for shortest-path calculations on the application's configured graph.

The backend graph connects each fictional centre to its nearest neighbours. Route optimization and actual road routing are separate operations: a graph-based shortest path does not guarantee the fastest real-world road route.

Demonstration limitation: Public routing and map services may have usage restrictions, availability limitations, or geographic coverage differences. Only fictional coordinates should be used for this project.

8. Delivery Tracking System

The delivery module tracks incoming shipments through defined lifecycle states.

Delivery statuses:

PENDING → IN_TRANSIT → DELIVERED

An additional DELAYED status may be used when a shipment encounters a delay.

Key capabilities:

List incoming deliveries.

View shipment status.

Update delivery progress.

Display a shipment timeline.

Record delivery completion.

Update inventory when goods are received.

Inventory consistency: Delivery completion and inventory updates should occur in a single database transaction. Repeated delivery-completion requests must not add the same quantity to inventory more than once.

🧠 Machine Learning Pipeline

Data Generation

The project generates approximately 365 days of synthetic consumption history for each configured item and fictional supply-centre combination.

Synthetic records may include daily consumption patterns, trends, and controlled variations to support model development.

Feature Engineering

FeaturePurposeday_of_weekRepresents weekly demand patternsmonthRepresents seasonal or monthly variationlag_1Consumption on the previous daylag_7Consumption seven days earlierlag_14Consumption fourteen days earlierroll_mean_7Mean consumption over the previous seven daysroll_mean_14Mean consumption over the previous fourteen days

Rolling statistics must use historical observations only. Features should be shifted appropriately to avoid including the target day's consumption.

Model Training

The training pipeline follows these steps:

Load synthetic consumption history.

Sort records chronologically.

Generate lag and rolling-window features.

Split the dataset chronologically.

Train a Random Forest regression model.

Compare results with Linear Regression and a naive baseline.

Evaluate predictions using MAE and RMSE.

Save the selected model as demand_model.joblib.

Model Evaluation Metrics

Mean Absolute Error (MAE)

MAE=1n∑i=1n∣yi−y^i∣MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i-\hat{y}_i|

Root Mean Squared Error (RMSE)

RMSE=1n∑i=1n(yi−y^i)2RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y}_i)^2}

Where:

yiy_i represents actual demand.

y^i\hat{y}_i represents predicted demand.

nn represents the number of evaluated observations.

Lower MAE and RMSE values generally indicate smaller prediction errors on the evaluated dataset.

Forecast Inference

The application supports recursive forecasting:

Load recent historical consumption.

Generate features for the next day.

Predict demand.

Append the prediction to the working history.

Generate features for the following day.

Repeat until the requested forecast horizon is reached.

Recursive predictions can accumulate errors over longer horizons, so evaluation should reflect the same forecasting approach used in production.

🗺️ GIS and Route Planning

The GIS subsystem combines geospatial calculations with map-based route visualization.

Haversine Distance

The Haversine formula estimates the great-circle distance between two geographic coordinates.

a=sin⁡2(Δϕ2)+cos⁡(ϕ1)cos⁡(ϕ2)sin⁡2(Δλ2)a = \sin^2\left(\frac{\Delta\phi}{2}\right) + \cos(\phi_1)\cos(\phi_2) \sin^2\left(\frac{\Delta\lambda}{2}\right) d=2Rarcsin⁡(a)d = 2R\arcsin(\sqrt{a})

Where:

ϕ1,ϕ2\phi_1,\phi_2 are latitudes in radians.

Δϕ\Delta\phi is the latitude difference.

Δλ\Delta\lambda is the longitude difference.

RR is the Earth's mean radius.

dd is the estimated surface distance.

Dijkstra's Algorithm

Dijkstra's algorithm calculates the lowest-cost path in a weighted graph with non-negative edge weights.

In this demonstration, graph edges may be weighted using estimated travel times. The resulting route depends on the graph construction and edge-weight assumptions.

OSRM Integration

The frontend or backend can request road geometry from the OSRM service for fictional demonstration points. The returned geometry can then be rendered on the interactive map.

The system should handle failed requests, invalid coordinates, unavailable routes, and public-service rate limitations gracefully.

🌦️ Weather Risk Analysis

The weather risk engine combines a base weather score with configurable modifiers.

Illustrative base scores may include:

Simulated ConditionExample Base ScoreClear5Moderate rainConfigurableHeavy rain65Snow or severe conditionsConfigurable

Additional modifiers may be applied for:

Wind speeds above the configured threshold.

Visibility below the configured threshold.

Extreme temperatures.

Other supported adverse weather indicators.

The resulting score is clamped to the range 0–100.

Risk classification:

LOW: 0–24

MEDIUM: 25–44

HIGH: 45–69

CRITICAL: 70–100

These values are demonstration rules, not validated military transport or safety standards.

🛠️ Technology Stack

LayerTechnologiesFrontendReact 19, ViteRoutingReact RouterHTTP ClientAxiosChartsRechartsInteractive MapsLeafletBackendPython 3.12, FastAPIASGI ServerUvicornData ValidationPydantic v2ORMSQLAlchemyDatabaseMySQL 8.0Database DriverPyMySQLMachine LearningScikit-learnData ProcessingPandas, NumPyModel PersistenceJoblibAuthenticationJWT, python-josePassword HashingBcrypt, PasslibWeather APIOpenWeatherMapRoad RoutingOSRMStreet MapsOpenStreetMapSatellite MapsEsriTerrain MapsOpenTopoMap

🏗️ System Architecture

The application follows a frontend-backend-database architecture.

flowchart TD A[User] --> B[React Frontend] B --> C[FastAPI Backend] C --> D[JWT Authentication and RBAC] C --> E[Inventory and Delivery Services] C --> F[Machine Learning Forecasting] C --> G[Weather and GIS Services] E --> H[(MySQL Database)] F --> I[Saved ML Model] F --> H G --> J[External Map, Routing and Weather APIs] D --> H E --> B F --> B G --> B 

Request Workflow

A user logs in through the React frontend.

The backend validates the credentials and issues a JWT.

The frontend sends the token with protected API requests.

FastAPI validates authentication and role permissions.

Application services process inventory, forecasting, weather, or delivery requests.

SQLAlchemy interacts with MySQL.

The backend returns structured responses.

The frontend displays the results through dashboards, charts, tables, and maps.

🗄️ Database Schema

The application uses MySQL 8.0 with SQLAlchemy ORM.

Core Tables

TablePurposeusersStores user account informationrolesDefines supported access rolessupply_centresStores fictional centre names, codes, coordinates, and regionssupply_itemsStores item names, SKUs, units, and categoriesinventory_balancesMaintains current quantities and safety-stock valuesstock_transactionsRecords stock-in and stock-out movementsconsumption_historyStores synthetic daily consumption recordsincoming_deliveriesTracks shipment quantities, statuses, and delivery information

Suggested Relationships

Users are associated with their assigned roles.

Each inventory balance references a supply item and a supply centre.

Each stock transaction references the affected inventory record and, where applicable, the responsible user.

Consumption records reference a supply item and a supply centre.

Incoming deliveries reference their associated items and destination centres.

Foreign keys, appropriate indexes, unique constraints, and database transactions should be implemented to preserve data integrity.

🔌 API Documentation

The backend exposes REST API endpoints through FastAPI.

Base URL: http://localhost:8000/api

Authentication APIs

MethodEndpointDescriptionPOST/api/auth/loginAuthenticate a user and obtain a JWTGET/api/auth/meRetrieve the current user profilePOST/api/auth/change-passwordChange the authenticated user's passwordGET/api/usersList users (ADMIN only)POST/api/usersCreate a user (ADMIN only)

Inventory and Delivery APIs

MethodEndpointDescriptionGET/api/inventoryRetrieve inventory balancesPOST/api/transactionsRecord a stock-in or stock-out transactionGET/api/deliveriesRetrieve incoming deliveriesPUT/api/deliveries/{id}Update a delivery's status

AI/ML and Analytics APIs

MethodEndpointDescriptionGET/api/forecast/{item_id}?centre_id={id}&days=7Generate a 7-day forecastGET/api/forecast/{item_id}?centre_id={id}&days=30Generate a 30-day forecastGET/api/shortage-analysis?horizon_days=7Analyze shortages over 7 daysGET/api/shortage-analysis?horizon_days=30Analyze shortages over 30 daysGET/api/weather/overviewRetrieve weather and delay-risk summariesGET/api/routes?source={code}&destination={code}Calculate and retrieve route information

Interactive API documentation: http://localhost:8000/docs

The endpoint list describes the intended API contract. Actual response schemas, accepted values, and authorization rules should be verified against the implemented FastAPI routes.

📂 Project Structure

The following is a suggested project structure. Adjust the file names to match the actual repository.

predictive-logistics/ │ ├── backend/ │ ├── app/ │ │ ├── main.py │ │ ├── models/ │ │ ├── schemas/ │ │ ├── routes/ │ │ ├── services/ │ │ ├── core/ │ │ └── database.py │ │ │ ├── scripts/ │ │ ├── seed_initial_data.py │ │ ├── enhance_demo_data.py │ │ ├── generate_consumption.py │ │ └── train_model.py │ │ │ ├── requirements.txt │ ├── .env.example │ └── .gitignore │ ├── frontend/ │ ├── src/ │ │ ├── components/ │ │ ├── pages/ │ │ ├── services/ │ │ ├── hooks/ │ │ └── App.jsx │ │ │ ├── public/ │ ├── package.json │ ├── .env.example │ └── .gitignore │ ├── docs/ │ ├── architecture.md │ └── database-schema.md │ ├── README.md └── LICENSE 

💻 Prerequisites

Install the following software before running the application:

Python 3.10 or later — Python 3.12 is recommended for this stack.

Node.js 18 or later — use a version compatible with the installed Vite dependencies.

MySQL 8.0 or later.

Git — recommended for source control.

MySQL Workbench — optional graphical database management tool.

Verify the installations:

python --version node --version npm --version git --version 

⚙️ Installation and Setup

The following instructions are for Windows PowerShell.

Step 1: Clone the Repository

If the project is hosted on GitHub, run:

git clone <YOUR_REPOSITORY_URL> cd predictive-logistics 

Replace the placeholder with the actual repository URL. If the source code is already on your computer, navigate directly to the project folder.

Step 2: Create the MySQL Database

Open MySQL Workbench or the MySQL command-line client and execute:

CREATE DATABASE predictive_logistics CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
