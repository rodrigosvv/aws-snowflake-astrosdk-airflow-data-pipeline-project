# Airflow Data Pipeline con AWS y Snowflake

El objetivo del proyecto es crear un flujo de datos completamente funcional que interactúa con Snowflake y AWS utilizando Astro SDK. El proyecto busca proporcionar experiencia práctica en la configuración del entorno de Airflow, la carga de datos en S3, la configuración de Snowflake e implementar diversas tareas de flujo de datos como carga, filtrado, unión, fusión, transformación y limpieza de datos.

## Pre-requisitos

- Tener instalado Astro CLI
- Tener instalado Docker 

## Tech Stack
- <img alt="Python" src="https://img.shields.io/badge/Python-_?logo=python&color=white" />
- <img alt="S3" src="https://img.shields.io/badge/Amazon%20S3-_?logo=amazons3&logoColor=white&color=%23569A31">
- <img alt="Snowflake" src="https://img.shields.io/badge/Snowflake-_?logo=snowflake&logoColor=white&color=%2329B5E8" /> 
- <img alt="Static Badge" src="https://img.shields.io/badge/Astronomer%20Cosmos-_?logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyBoZWlnaHQ9IjMwMCIgdmlld0JveD0iMCAwIDMwMCAzMDAiIHdpZHRoPSIzMDAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPjxsaW5lYXJHcmFkaWVudCBpZD0iYSIgeDE9IjIwLjAwNzI2NCUiIHgyPSI4Mi4xOTA0MTclIiB5MT0iLTUuNTMwODkxJSIgeTI9Ijg5LjMwMzM5NSUiPjxzdG9wIG9mZnNldD0iMCIgc3RvcC1jb2xvcj0iIzk0NzhkMiIvPjxzdG9wIG9mZnNldD0iMSIgc3RvcC1jb2xvcj0iIzU5NDE4ZCIvPjwvbGluZWFyR3JhZGllbnQ%2BPHBhdGggZD0ibTE0Ni4wODY2NDcuMDgxNTQ2MzZjLTQwLjMyNTE3OSAxLjMwNTc0ODUyLTc3LjcyNTc2MjggMTguMjM0MTY4OTQtMTA1LjMxNjYyMTYgNDcuNjcwMzkxNjQtNTYuOTU1NjAyNSA2MC43NjYxMzMtNTMuODU0ODI3MyAxNTYuNTM5ODE3IDYuOTA5MjkyMyAyMTMuNDk2NDI2IDIxLjMxMzgwMjUgMTkuOTc1ODM4IDQ2Ljk0MzUyMTYgMzIuNTMzOTc4IDczLjY4NjcwMTMgMzcuODM3NTExbDguMDE1NzA1LTIwLjA0MjI4M2MtMjQuMzg1MzgyLTQuMDc0Mjk4LTQ3Ljg2ODcyMDYtMTUuMTA5MjMyLTY3LjIyMDM3NjctMzMuMjQ2NzUzLTUyLjI0MzAyODI5LTQ4Ljk3MTEwNy01NC45MDg4ODk1Ni0xMzEuMzE0ODA5LTUuOTM5Nzk2Ni0xODMuNTU5ODUxMiAyMy43MjI5NDM3LTI1LjMwODU2NzQgNTUuODgwMzk4My0zOS44NjcxMDk2IDkwLjU1MDY4OTMtNDAuOTg4NjIzOCAxLjQzNzYzMi0uMDQ3MzE3IDIuODc0MjU4LS4wNjg0NTg2IDQuMzA3ODYzLS4wNjg0NTg2IDI2LjE1MDIwNiAwIDUxLjIwMDA0IDcuNzU2OTcxNyA3Mi41MzQ5ODQgMjIuMjIxODg2Nmw4LjAyNzc4Ny0yMC4wNzQ0OTkxYy0yMy45NjU1Ny0xNS4yMDY4ODYxNy01MS42ODYyOTktMjMuMzI3MjkyOS04MC41NDg2NzctMjMuMzI3MjkyOS0xLjY2NjE2MyAwLTMuMzM0MzQuMDI3MTgyMTItNS4wMDc1NS4wODE1NDYzNnptMTUuMjg4NDMyIDc2LjYzNzQ3MTA0aC0yMC4zMzcyNTktLjY4MTU2N2wtLjI1MzcuNjMzMjQyNy01My41MTQ1NDcxIDEzMy43ODUzNjE5LS41NTE2OTY0IDEuMzgxMjU0aDEuNDg2OTYyNyAyMS41OTc3MDQ4LjY4ODYxNGwuMjQ4NjY2LS42NDIzMDMgMTMuMTI5OTctMzMuNzYwMTkzaDU3LjcwNTYyOGwxMy4yOTUwNzcgMzMuNzY1MjI3LjI1MDY4LjYzNzI2OWguNjg2NiAyMi4zNjA4MTcgMS40ODY5NjNsLS41NTI3MDMtMS4zODEyNTQtMzQuNTU0NTE1LTg2LjM4Njc5MS0uMjUyNjkzLS42MzIyMzZoLS42ODI1NzQtMjEuNjE5ODUzLTEuNDcxODYxbC41MzM1NzUgMS4zNzExODcgMTIuMjU2MTE2IDMxLjUwMTA1N2gtNDEuMDEyNzg2bDMwLjY5NzY3NS03OC44OTk2Mjc5LjUzMzU3NS0xLjM3MjE5Mzd6IiBmaWxsPSJ1cmwoI2EpIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE3LjI1KSIvPjwvc3ZnPg%3D%3D&color=%23D6D6D6"/>
- <img alt="Docker" src="https://img.shields.io/badge/Docker-_?logo=docker&color=lightblue" />
- Airflow

## Setup de Airflow

### Iniciamos el proyecto mediante Astro CLI

![Astro init CMD](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/8a54188b-08d5-4f99-acdc-2a42f62b685c)

### Instalamos AstroSDK con los providers de Amazon y Snowflake

![Requirements](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/2d289bc2-c7f9-4632-a170-2106daa3ff1f)

### Variables de entorno

![env](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/5602d760-88b2-4a59-acf2-5b3cec41f114)

### orders_data_header.csv

![csv](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/48a28052-467c-409c-9661-69f3b0abb53d)

## AWS S3 e IAM

### Creamos un S3 bucket y subimos orders_data_header.csv

![AWS Bucket y Archivo CSV](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/bc74d625-8330-4bc3-94d0-3205b071897b)

### Creamos un usuario, damos el rol de AdministratorAccess y asignamos una Access Key (IAM)

![AWS IAM user](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/99d12f00-4646-414d-8755-3ecf699108da)

## Snowflake: DB, Schema, DW, Customers Table y Orders Table

### Schema

![Snowflake Schema](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/8d4f73aa-2c0c-4151-868d-9b1762280502)

### Data Warehouse

![Snowflake Astro WH](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/b1e3859e-9ce2-4d9b-b1e9-7da064caea13)

### Tables

![Table](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/05f7af56-4014-49a0-ad8f-05e04c15a8e1)

## Creamos las conexiones correspondientes

### AWS 

![AWS Conn](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/1f70f5f3-225e-48c8-ac0b-6a99e643809b)

### Snowflake

![Snowflake Conn](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/84bb2e7d-36e5-4fd5-8505-7bc7cc5f1b20)

## Creamos el Data Pipeline: astro_orders.py

Cargaremos el archivo del S3 bucket a una tabla, filtraremos las órdenes de esa tabla y las uniremos con los clientes. Luego, fusionaremos los datos en la tabla de informes y, finalmente, transformaremos los datos dentro de esta tabla para obtener las fechas de compra. Para concluir, eliminaremos todas las tablas temporales creadas durante el proceso.

### Imports y Variables

![Imports y Variables](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/f79c6285-4a6b-47c1-893f-b9e0c4d12451)

### AQL 

![AQL](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/63987f04-acdf-4e4d-9ccf-505415576380)

### DAG, Tasks y Dependencias

![DAG, Tasks y Dependencies](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/a06224f6-006d-4cf3-b7db-84282c77a5bf)

### ¡Data Pipeline en acción!

![Pipeline Success](https://github.com/rodrigosvv/aws-snowflake-astrosdk-airflow-data-pipeline-project/assets/143859478/f1e1fa50-5b5b-4190-a9c7-b1f880e07c64)

