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
- Libraries: `pandas`, `langchain_community`, `langchain_core`, `langchain_openai` (the `sqlite3` module is included with Python)

#### Installation

1. **Clone the Repository**:
   - Clone this repository to your local machine to get started with the script.

2. **Set Up the Environment**:
   - Ensure Python 3.11.4 is installed on your system.
   - Install the required Python libraries using pip:
     ```
     pip install pandas langchain_community langchain_core langchain_openai
     ```

3. **Run the Script**:
   - Navigate to the directory containing the notebook.
   - Launch the notebook in a Jupyter environment.
   - Execute the notebook cells sequentially to import the data, set up the database, and begin querying using natural language.
  
```python
from operator import itemgetter

from langchain_core.output_parsers import StrOutputParser
from langchain_core.prompts import PromptTemplate
from langchain_core.runnables import RunnablePassthrough

prompt_query_answer = PromptTemplate.from_template(
    """Given the following user question, corresponding SQL query, and SQL result, answer the user question.

Question: {question}
SQL Query: {query}
SQL Result: {result}
Answer: """
)

answer = prompt_query_answer | llm | StrOutputParser()
chain = (
    RunnablePassthrough.assign(query=write_query).assign(
        result=itemgetter("query") | execute_query
    )
    | answer
)

chain.invoke({"question": "List top 10 projects with the highest number of forks"})
```

```python
Output: 'The top 10 repositories with the highest number of forks are:\n\n1. ChatGPT-Next-Web with 54,259 forks\n2. generative-ai-for-beginners with 21,598 forks\n3. awesome-machine-learning with 14,447 forks\n4. langchain with 12,434 forks\n5. Flowise with 11,784 forks\n6. llama.cpp with 7,703 forks\n7. awesome-cpp with 7,613 forks\n8. private-gpt with 6,804 forks\n9. chatgpt-on-wechat with 6,622 forks\n10. lobe-chat with 5,941 forks'
```

#### Conclusion

This script provides a user-friendly interface for querying GitHub repository data using advanced NLP techniques. By simplifying data query operations through natural language inputs, it makes data accessibility easier for users without extensive SQL knowledge, making it an ideal tool for data analysis and educational purposes.
