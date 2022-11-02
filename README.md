# **ScarletCourse**
An aggregator for the Rutgers SOC API with a more simpler developer experience. This is a project built for parsing courses for [**Scarlet Navigator**](https://scarletnav.io). It prevents potential overriding conflicts when compiling courses for both Spring and Fall semesters, while adding important metadata for the **Scarlet Navigator** project.

# Getting Started
Make sure you have the following installed:
- [Python 3.6+](https://www.python.org/downloads/)
- [Pip3](https://pip.pypa.io/en/stable/installing/)
- [Git](https://git-scm.com/downloads)

```bash
git clone git@github.com:openscarletorg/ScarletCourse.git
cd ScarletCourse
pip3 install -r requirements.txt
```

# Use case
To run the scraper, you need to specify the year and semester you want to scrape. The scraper will scrape all the courses for that semester and store them in a `json` file.

```bash
python3 scraper.py [year] [semester]
```
```bash
python3 scraper.py 2019 fall-spring -o output.json
```
The above command will scrape all the courses for the Fall 2019 semester and Spring 2020 semester, storing them in `output.json`.

If there are conflicts (duplicate courses) between the two semesters, the scraper will automatically add to the course metadata with important information distinguishing between Fall and Spring. The scraper will then store the courses in the `json` file.

Following values for `semester` are supported:
- `fall`
- `spring`
- `winter`
- `summer`
- `fall-spring`
- `fall-winter-spring`
- `summer-fall-winter-spring`

## Considerations
Before the scraper calls the SOC API, it will first make sure the parameters are valid. If the year is currently 2025 but semester data for Spring is not ready, it will not run.

## Further Examples
Following command creates an output.json file with all the courses for the Fall 2019 semester for undergrad courses in Camden.
```bash
python3 scraper.py 2019 fall -o output.json -p cam -l undergrad
```

## Description
You can specify the following options:
- `--output` or `-o`: The output file to store the scraped data in. Defaults to `output.json`
- `--level` or `-l`: The level of the courses to scrape. Defaults to `undergraduate`.
  - `undergrad`: Scrape all undergraduate courses
  - `grad`: Scrape all graduate courses
  - `all`: Scrape both grad and undergrad courses
- `--place` or `-p`: Whether to print the scraped data to the console. Defaults to `False`
  - `nb`: Scrape New Brunswick courses
  - `cam`: Scrape Camden courses
  - `newark`: Scrape Newark courses
  - `online`: Scrape online courses
  - `all`: Scrape courses from all campuses/locations
- `--verbose` or `-v`: Whether to print course titles and conflict management to console. Defaults to `False`
- `--help` or `-h`: Show the help message and exit