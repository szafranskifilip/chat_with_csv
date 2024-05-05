## Chat with your CSV file Using LangChain and OpenAI

#### Overview

This script demonstrates a sophisticated approach to querying a SQLite database by integrating the LangChain library with OpenAI's API to perform text-to-SQL translation. The primary objective is to provide an interactive way to explore GitHub repository data using natural language queries that are automatically converted into SQL queries. This process facilitates easy retrieval of data without requiring deep SQL expertise.

#### Features

- **Data Importation**: Imports GitHub repository data from a CSV file into a SQLite database, utilizing pandas for data processing and sqlite3 for database management.
- **LangChain Integration**: Leverages LangChain to dynamically generate SQL queries from natural language inputs.
- **OpenAI API Usage**: Utilizes OpenAI's powerful model capabilities to interpret natural language and generate corresponding SQL queries.
- **Text-to-SQL Conversion**: Implements a text-to-SQL technique allowing users to ask questions directly and receive data-driven answers based on the content of the SQLite database.
- **Data Retrieval**: Executes SQL queries generated from natural language questions to fetch data about the most forked GitHub projects, showcasing the top repositories directly from the notebook.

#### Workflow

1. **Data Setup**:
   - Data is loaded from `data/github_final.csv` into a pandas DataFrame.
   - DataFrame is then exported to a SQLite database `data/github_final.db`.

2. **Query Processing**:
   - A LangChain chain is configured with a natural language prompt template to guide the conversion of user questions into SQL.
   - The OpenAI API (specifically using the `gpt-3.5-turbo-0125` model) processes the input and generates a syntactically correct SQL query.
   - The SQL query is executed against the SQLite database to retrieve data.

3. **Output Generation**:
   - Results from the SQL queries are parsed and formatted to provide a clear, readable answer to the user's question, such as listing the top 10 GitHub projects by the number of forks.

#### Prerequisites

- Python 3.11.4
- Libraries: `sqlite3`, `pandas`, `langchain_community`, `langchain_core`, `langchain_openai`

#### Installation

1. **Clone the Repository**:
   - Clone this repository to your local machine to get started with the script.

2. **Set Up the Environment**:
   - Ensure Python 3.11.4 is installed on your system.
   - Install the required Python libraries using pip:
     ```
     pip install sqlite3 pandas langchain_community langchain_core langchain_openai
     ```

3. **Run the Script**:
   - Navigate to the directory containing the notebook.
   - Launch the notebook in a Jupyter environment.
   - Execute the notebook cells sequentially to import the data, set up the database, and begin querying using natural language.

#### Conclusion

This script provides a user-friendly interface for querying GitHub repository data using advanced NLP techniques. By simplifying data query operations through natural language inputs, it makes data accessibility easier for users without extensive SQL knowledge, making it an ideal tool for data analysis and educational purposes.
