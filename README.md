# CPSC 319

This repo is for code examples and what not.

## Authentication Example

In production your application will be running in an Apache Tomcat servlet container. Your application is not responsible for authentication but you will need to get the logged in user's id.

This example shows how to get the user id in the production envirnonment using a "bare bones" servlet (ie. no framework). It also shows how you might mock this out in your development and/or testing environments. The important thing to note is that you can switch from/to production/development with just a small change to the config.

If you're using a framework such as Jersey or Spring you'll need to figure out how to do the equivalent.

This is a maven project that has been set up to run in eclipse as a dynamic web application [Example Setup](https://wiki.base22.com/display/btg/How+to+create+a+Maven+web+app+and+deploy+to+Tomcat+-+fast).


When running in development and/or test the web.xml should use the "DevelopmentIdentityFilter". For example:

```
...
  <filter>
   <filter-name>Identity Filter</filter-name>
   <filter-class>ca.ae.cpsc319.DevelopmentIdentityFilter</filter-class>
  </filter>
  
  <filter-mapping>
   <filter-name>Identity Filter</filter-name>
   <servlet-name>ca.ae.cpsc319.ExampleServlet</servlet-name>
  </filter-mapping>  
...
```

Using the DevelopmentIdentityFilter you can specify the uid in the query parameters:

```
http://localhost:8080/example?uid=goulets
```

If you'd like to test out the ProductionIdentityFilter you can configure your applicaiton to use Basic Authentication. I'll leave this as an exercise.
