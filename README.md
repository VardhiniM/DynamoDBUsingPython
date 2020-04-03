# DynamoDB_using_Python

## Data Sources
Mocked up data based on data scraped from Indeed website. I extracted the following pieces of information: the “Job Title”, the “Company Name”, and the location as “City”, “State”, and “ZipCode” (if available), “Reviews” (if available). Then we consolidated the rest of the contents into a single text blob named as the “Job Description”. We then parsed the description to extract the pay information as “Salary”, if provided.

## Explanation of the Database Design Choices and Advantages Over Alternatives
I chose to use DynamoDB, a NoSQL database, because of the nature of the data that I worked with. As it is text-intensive data, I selected a NoSQL format over a traditional relational database.

NoSQL gave the flexibility to add and remove attributes as I did not have to define the structure beforehand. Most of the job descriptions contained data for fields like title, company name, city/state, and few of them had information about the zip code, salary, reviews, etc. The NoSQL database enables us to store the entire job description in a column, which would be a bad design choice for a structured database.

I had to define the partition key and sort key for the table in DynamoDB which is analogous to the primary key in SQL. I had to combine columns that would be unique for each record, and I also had to consider the ways in which we would access the data to decide our partition and sort keys. Since we will primarily be working with job titles, I chose that to be the partition key. The other key column we will access is the location so we could define that as our sort key. But the issue is that the combination of title and location will not be unique for each item. So, I decided to combine the company name with the location for our sort key. We could create secondary indexes for other columns if needed.
