---
layout: post
title:  "Using XML in SpringBoot REST API"
date:   2023-09-19 17:55:00 +0100
categories: springboot
tags: [springboot, xml, rest api]
---

By default SpringBoot REST APIs use JSON to send and receive data.  But with a few small changes it is possible to use XML as well.

The following guide is for SpringBoot 3.x.

<!--more-->

## Adding support for XML

First we need to add a new dependency to our `pom.xml` file:

```xml
    <dependency>
        <groupId>com.fasterxml.jackson.dataformat</groupId>
        <artifactId>jackson-dataformat-xml</artifactId>
    </dependency>
```

or if we are using Gradle:
    
```groovy
    implementation 'com.fasterxml.jackson.dataformat:jackson-dataformat-xml'
```

Next we need to tell our endpoints to produce XML as well as JSON.  We can do this by adding the following annotation to the endpoints of our controller class (or amending the existing if you are already using it):

```java
    @RequestMapping(produces = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE})
```

By default, the endpoint will return the data in JSON format, but if the client sends an `Accept` header with a value of `application/xml` then the endpoint will return the data in XML format.

If we want our controller to accept XML data as well as JSON, then we need to add the following annotation to the controller class:

```java
    @RequestMapping(consumes = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE})
```

The controller is smart enough to determine the type of data being received, but to be safe we should add `Content-Type` header with a value of `application/xml` to the request.

## Renaming List elements

If your endpoint returns a List<> object, you may see the following in your XML response:

```xml
    <list>
        <item>...</item>
        <item>...</item>
        <item>...</item>
    </list>
```

To rename the elements, create a wrapper list class for your entities and use the @JacksonXmlRootElement and @JacksonXmlProperty anotations to configure the XML output.  

For example, if we have an endpoint that returns a list of MovieDataModel entities:

```java
    @GetMapping(value = "/movies", produces = { MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE })
    public List<MovieDataModel> getAllMovies() {
        return repository.findAll();
    }
```

First, add the following class:

```java    
    import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlElementWrapper;
    import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlProperty;
    import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlRootElement;
    import java.util.List;

    @JacksonXmlRootElement(localName = "movies")
    public class MovieListDataModel {
        @JacksonXmlProperty(localName = "movie")
        @JacksonXmlElementWrapper(useWrapping = false)
        private final List<MovieDataModel> movies;

        public MovieListDataModel(List<MovieDataModel> movies) {
            this.movies = movies;
        }

        public List<MovieDataModel> getMovies() {
            return movies;
        }
    }
```

and change the return type to `MovieListDataModel`:

```java
    @GetMapping(value = "/movies", produces = { MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE })
    public MovieListDataModel getAllMovies() {
        return new MovieListDataModel(repository.findAll());
    }
```

This will produce the following XML:

```xml
    <movies>
        <movie>...</movie>
        <movie>...</movie>
        <movie>...</movie>
    </movies>
```

And it will still return valid JSON.

## Further Reading
- [Sample Rest Api Repository](https://github.com/zjcz/sample-rest-service){:target="_blank"}
- [Stackoverflow: Spring Boot XML serialisation of List query](https://stackoverflow.com/questions/60020978/spring-boot-xml-serialisation-of-list-query){:target="_blank"}

