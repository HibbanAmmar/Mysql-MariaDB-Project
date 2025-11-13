<h3 align="center">COVID-19 DATABASE</h3>

  <p align="center">
    Latihan Mysql/MariaDB.
    <br />
    <a href="https://www.kaggle.com/code/franklinposso/sql-project-exploratory-analysis-covid-19"><strong>Klik untuk detail yang lebih lengkap</strong></a>
    <br />
  </p>
</p>

## Tentang Latihan

Latihan ini dirancang sebagai latihan hands-on untuk menguasai SQL (Structured Query Language) menggunakan sistem basis data populer, MySQL dan MariaDB. Daripada menggunakan data contoh yang abstrak, kita akan menggunakan dataset COVID-19 yang nyata, kompleks, dan relevan untuk melatih kemampuan query dan analisis data.

---

## Tutorial

Berikut langkah-langkah untuk menginstal dan menjalankan projek ini di Linux.

1.  **Clone repositori ini**
    ```sh
    git clone https://github.com/iblazz-py/Mysql-MariaDB-Project.git
    ```
2.  **Pindah ke direktori proyek**
    ```sh
    cd Mysql-MariaDB-Project
    ```
3.  **Buat Database**
    ```sh
    CREATE DATABASE covid_db
    ```
4.  **Buat Table covid_deaths**
    ```sh
    CREATE TABLE covid_db.covid_deaths (
    iso_code TEXT,
    continent TEXT,
    location TEXT,
    date TEXT,
    population BIGINT,
    total_cases BIGINT,
    new_cases BIGINT,
    new_cases_smoothed FLOAT,
    total_deaths BIGINT,
    new_deaths BIGINT,
    new_deaths_smoothed FLOAT,
    total_cases_per_million BIGINT,
    new_cases_per_million BIGINT,
    new_cases_smoothed_per_million BIGINT,
    total_deaths_per_million BIGINT,
    new_deaths_per_million BIGINT,
    new_deaths_smoothed_per_million FLOAT,
    reproduction_rate BIGINT,
    icu_patients BIGINT,
    icu_patients_per_million BIGINT,
    hosp_patients BIGINT,
    hosp_patients_per_million BIGINT,
    weekly_icu_admissions BIGINT,
    weekly_icu_admissions_per_million BIGINT,
    weekly_hosp_admissions BIGINT,
    weekly_hosp_admissions_per_million BIGINT
    );
    ```
4.  **Buat Table Covid_Vaccination**
    ```sh
    CREATE TABLE covid_db.covid_vaccination (
    iso_code TEXT,
    continent TEXT,
    location TEXT,
    date TEXT,
    new_tests BIGINT,
    total_tests BIGINT,
    total_tests_per_thousand BIGINT,
    new_tests_per_thousand BIGINT,
    new_tests_smoothed BIGINT,
    new_tests_smoothed_per_thousand FLOAT,
    positive_rate FLOAT,
    tests_per_case FLOAT,
    tests_units BIGINT,
    total_vaccinations BIGINT,
    people_vaccinated BIGINT,
    people_fully_vaccinated BIGINT,
    new_vaccinations BIGINT,
    new_vaccinations_smoothed BIGINT,
    total_vaccinations_per_hundred FLOAT,
    people_vaccinated_per_hundred FLOAT,
    people_fully_vaccinated_per_hundred FLOAT,
    new_vaccinations_smoothed_per_million BIGINT,
    stringency_index FLOAT,
    population_density FLOAT,
    median_age FLOAT,
    aged_65_older FLOAT,
    aged_70_older FLOAT,
    gdp_per_capita FLOAT,
    extreme_poverty FLOAT,
    cardiovasc_death_rate FLOAT,
    diabetes_prevalence FLOAT,
    female_smokers FLOAT,
    male_smokers FLOAT,
    handwashing_facilities FLOAT,
    hospital_beds_per_thousand FLOAT,
    life_expectancy FLOAT,
    human_development_index FLOAT,
    excess_mortality FLOAT
    );
    ```
4.  **Load CSV File ke dalam Database covid_db**
    ```sh
    1. LOAD DATA LOCAL INFILE 'PATH/covid_deaths.csv' INTO TABLE covid_deaths CHARACTER SET UTF8 FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\r\n' IGNORE 1 LINES;
    2. LOAD DATA LOCAL INFILE 'PATH/covid_vaccination.csv' INTO TABLE covid_vaccination CHARACTER SET UTF8 FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\r\n' IGNORE 1 LINES;
---

## Analisis Data
**Untuk covid_deaths**

SELECT date, continent, location, total_cases, new_cases, total_deaths, population
FROM covid_db.covid_deaths
ORDER BY location, date;

**Untuk covid_vaccination**

SELECT deaths.continent, deaths.location, deaths.date, vaccination.new_vaccinations,
AVG(vaccination.new_vaccinations) OVER (PARTITION BY deaths.location ORDER BY deaths.date) as RollingAvg_Vaccines
FROM covid_db.covid_deaths deaths
JOIN covid_db.covid_vaccination vaccination
ON deaths.location = vaccination.location
AND deaths.date = vaccination.date
WHERE deaths.continent = 'Europe'
ORDER BY location, date;



