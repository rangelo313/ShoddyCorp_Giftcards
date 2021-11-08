# Part Two 


Looking at the instructions it looks like we are needed to do a migration with kubernetes jobs. 

To do this we must create a yaml file to integrate using django's migration functionality. In order to successfully do this, we must assign execute permissions and enter the following: 

Kubectl apply –f integration.yaml  

 Python manage.py migrations will seem like django can do this job for us. 

The setup.sql script seems to be performing the database migrations from the models file and seeds the database to populate it with data.  

 I modify db/Dockerfile to remove the lines that performs the migrations and database seeding similtaneously. This requires use to comment/remove lines from the Dockerfile. 
`COPY ./products.csv /products.csv
COPY ./users.csv /users.csv
#COPY ./setup.sql /docker-entrypoint-initdb.d/setup.sql
COPY ./db-seed.sql /docker-entrypoint-initdb.d/db-seed.sql
ENTRYPOINT ["/entrypoint.sh"]
CMD ["mysqld", "--secure-file-priv=/"]
#CMD ["--secure-file-priv=/"]
`
 