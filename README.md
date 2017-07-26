# file-to-ldap-lookup
"- Open a delimited file. Lookup LDAP data based on a field in the file. Output the data to a file or console."

The scenario I built includes:

OpenLdap in Docker image.  Can be created using this command:
docker run --name my-openldap-container -p 389:389 --detach osixia/openldap:1.1.9

Then I ran the src/main/resources/ldap.ldif agains the LDAP instance in docker to populate with 3 names in the people group

The test input, archive and output locations are in src/test/resources/[input|archive|output] respectively.

I've externalized the properties in mule-app.properties file.

The flow goes like this:
-Reads in the input csv file
-transforms the rows into an arraylist 
-runs through a foreach to look up by "name" filter in ldap
-transforms the response from ldap to include original data from csv and writes to a file, then to the logger.
-iterates through the array(3) and appends the transformed output to the file until done.
-done
