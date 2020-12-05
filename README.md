# Demonstrates compilation error with graphql-maven-plugin

Using this graphql schema:

```graphql

scalar DateTime

input DateTimeFilter {
    eq: DateTime
    le: DateTimes
    lt: DateTime
    ge: DateTime
    gt: DateTime
}

type DEntry {
    id: ID!
    type: String
    createdAt: DateTime
    updatedAt: DateTime
    deletedAt: DateTime
    license: String
    source: String
    sourceUrl: String
    sourceId: String
    translationExcerpt: String
}

input DEntryFilter {
    id: [ID!]
    createdAt: DateTimeFilter
    updatedAt: DateTimeFilter
    deletedAt: DateTimeFilter
    and: DEntryFilter
    or: DEntryFilter
    not: DEntryFilter
}

type Subscription {
    getDEntry(id: ID!): DEntry
    queryDEntry(filter: DEntryFilter): [DEntry]
}
```

When running

```
mvn clean compile
```

I get such errors:

```
[INFO] -------------------------------------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.028 s
[INFO] Finished at: 2020-12-05T11:29:41+01:00
[INFO] Final Memory: 35M/134M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.5.1:compile (java-compile) on project graphql-maven-bug: Compilation failure: Compilation failure: 
[ERROR] /Users/balazs/Documents/work/sztaki/szotar/sztakidict2020/trials/graphql-maven-bug/target/generated-sources/graphql-maven-plugin/test/client/util/SubscriptionExecutor.java:[611,56] no suitable method found for execute(com.graphql_java_generator.client.request.ObjectResponse,java.util.Map<java.lang.String,java.lang.Object>,com.graphql_java_generator.client.SubscriptionCallback<java.util.List<test.client.DEntry>>,java.lang.String,java.lang.Class<test.client.Subscription>,java.lang.Class<test.client.DEntry>)
[ERROR]     method com.graphql_java_generator.client.QueryExecutor.<R>execute(com.graphql_java_generator.client.request.AbstractGraphQLRequest,java.util.Map<java.lang.String,java.lang.Object>,java.lang.Class<R>) is not applicable
[ERROR]       (cannot infer type-variable(s) R
[ERROR]         (actual and formal argument lists differ in length))
[ERROR]     method com.graphql_java_generator.client.QueryExecutor.<R,T>execute(com.graphql_java_generator.client.request.AbstractGraphQLRequest,java.util.Map<java.lang.String,java.lang.Object>,com.graphql_java_generator.client.SubscriptionCallback<T>,java.lang.String,java.lang.Class<R>,java.lang.Class<T>) is not applicable
[ERROR]       (inference variable T has incompatible equality constraints test.client.DEntry,java.util.List<test.client.DEntry>)
[ERROR] /Users/balazs/Documents/work/sztaki/szotar/sztakidict2020/trials/graphql-maven-bug/target/generated-sources/graphql-maven-plugin/test/client/util/SubscriptionExecutor.java:[694,56] no suitable method found for execute(com.graphql_java_generator.client.request.ObjectResponse,java.util.Map<java.lang.String,java.lang.Object>,com.graphql_java_generator.client.SubscriptionCallback<java.util.List<test.client.DEntry>>,java.lang.String,java.lang.Class<test.client.Subscription>,java.lang.Class<test.client.DEntry>)
[ERROR]     method com.graphql_java_generator.client.QueryExecutor.<R>execute(com.graphql_java_generator.client.request.AbstractGraphQLRequest,java.util.Map<java.lang.String,java.lang.Object>,java.lang.Class<R>) is not applicable
[ERROR]       (cannot infer type-variable(s) R
[ERROR]         (actual and formal argument lists differ in length))
[ERROR]     method com.graphql_java_generator.client.QueryExecutor.<R,T>execute(com.graphql_java_generator.client.request.AbstractGraphQLRequest,java.util.Map<java.lang.String,java.lang.Object>,com.graphql_java_generator.client.SubscriptionCallback<T>,java.lang.String,java.lang.Class<R>,java.lang.Class<T>) is not applicable
[ERROR]       (inference variable T has incompatible equality constraints test.client.DEntry,java.util.List<test.client.DEntry>)
```


