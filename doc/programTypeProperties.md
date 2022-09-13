# Creating property files for program types

Specifying file properties in zAppBuild is typically done in `application-conf/file.properties`, where the syntax is to assign a property with the path name or path name pattern for the file(s) the property should be assigned to. However, some customers might be interested in defining a set of properties for a group of files that does not necessarily follow a path name pattern. For example, if your team's legacy build process used a processor group, you might want to preserve this behavior after migrating to a CI/CD pipeline with the DBB build tool. In this case, you can define a properties file containing multiple build properties inside the `build-conf` or `application-conf` folder, and then reference that properties file when defining the `programType` for the processor group. The following example illustrates how the properties of processor group PG1234 can be passed to the `programType` in the MortgageApplication sample.

1. Create a file named `PG1234.properties` that has the desired properties for processor group PG1234 in the `build-conf` or `application-conf` folder. For example, `PG1234.properties` could contain the following set of properties:

   ```
   cobol_compileOpts= TEST,...
   isMQ=true
   isDLI=true
   cobol_linkEditStream = INCLUDE ...
   ```

1. For each buildFile, introduce an individual file in the application's `properties` folder that just defines the `programType` with the same processor group name used in the previous step (in this case, `PG1234`). For example, the following snippet could be defined in `MortgageApplication/properties/programA.cbl.properties` to apply the PG1234 processor group to `programA.cbl` in the MortgageApplication:

    ```
    cobol_programType = PG1234
    ```
