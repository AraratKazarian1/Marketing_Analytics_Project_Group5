# ComboGenius 
## Problem

Many restaurants and food courts face challenges when it comes to expanding their corporate lunch service market through B2B websites. Despite offering great value and quality products, these businesses struggle with visibility among potential clients. The main issue lies in the lack of effective engagement strategies, making it difficult to showcase their benefits and attract new customers.

## Solution

To address this problem, a data-driven approach can be implemented across various restaurant and food court businesses. This approach involves two key strategies: enhancing product offerings by analyzing sales data and optimizing communication through targeted email interactions. Specific actions include gathering data on potential clients, analyzing customer preferences to develop appealing combos, and refining marketing communications to increase engagement rates.

## Expected Outcomes

Implementing these methods is expected to lead to increased corporate collaborations and improved interaction with potential B2B clients. Restaurants and food courts can anticipate greater customer satisfaction and higher conversion rates by customizing offerings and messaging based on data-driven insights. Moreover, these strategies can be applied beyond individual businesses, offering opportunities for improvement across the restaurant industry through metrics such as email campaign response rates and A/B testing results.

## Package Documentation
https://araratkazarian1.github.io/Marketing_Analytics_Project_Group5/

## API Endpoints
Endpoint to check if the FastAPI server is running - http://127.0.0.1:5000/ <br>
Endpoint to send an email to the specified recipient - http://127.0.0.1:5000/send_email/?recipient=ararat_kazarian%40edu.aua.am&subject=New%20Combo&discount=20 <br>
Endpoint to mark an email in the database as interested - http://127.0.0.1:5000/mark_interested/ararat_kazarian%40edu.aua.am <br>

## PyPi Link
https://pypi.org/project/combogenius/


## How to Use ComboGenius Package

### Import Necessary Functions
Begin by importing the required functions from the ComboGenius package. This includes functions related to database schema, SQL interactions, logger, and model for generating combos.
```python
from combogenius.database.schema import *
from combogenius.database.sql_interactions import SqlHandler
from combogenius.logger.logger import CustomFormatter
from combogenius.models.make_combos import combos
import pandas as pd
```

### Create and Load Data into Database
Before using ComboGenius, ensure your database tables follow this structure:
```python
class checks(Base):
    __tablename__ = "checks"

    check_number = Column(Integer, primary_key=True)
    products = Column(String)

class companies(Base):
    __tablename__ = "companies"

    company_id = Column(Integer, primary_key=True)
    link = Column(String)
    title = Column(String)
    phone = Column(String)
    address = Column(String)
    district = Column(String)
    email = Column(String)
    clicked = Column(Integer, default=0)

class price_list(Base):
    __tablename__ = "price_list"

    product_id = Column(Integer, primary_key=True)
    product = Column(String)
    price = Column(Integer)
```
Instantiate SqlHandler objects for each database table ('checks', 'companies', 'price_list'), and load the respective data into the database.
```python
Inst  = SqlHandler('database', 'checks')
Inst1 = SqlHandler('database', 'companies')
Inst2 = SqlHandler('database', 'price_list')

data = pd.read_csv('sample_data/data.csv')
companies = pd.read_csv('sample_data/companies.csv')
price_list = pd.read_csv('sample_data/price_list.csv')

Inst.insert_many(data)
Inst1.insert_many(companies)
Inst2.insert_many(price_list)

Inst.close_cnxn()
```

### Generate New Combos
Create an instance of the combos class and use the make_combos() method to generate new combinations. Pass the desired combo size as an argument to the make_combos() method.
```python 
m = combos()
f = m.make_combos(5)  # Generate combos of size 5
print(f)
```

### Visualize Combos
Utilize the visualization methods provided by the combos class to visualize the generated combos. You can visualize the most frequent combos, expensive combos, and cheap combos.
```python 
m.visualize_most_frequent_combos()
m.visualize_expensive_combos()
m.visualize_cheap_combos()
```
This guideline provides a basic framework for using the ComboGenius package, covering data loading, combo generation, and visualization of the results. Make sure to adjust paths and database configurations according to your specific setup.