﻿NHibernate Reliable SQL Azure Driver
====================================

Provides an NHibernate driver that uses the Microsoft Transient Fault Handling library to allow for reliable SQL Azure connections.

Using the provider when using Fluent NHibernate
-----------------------------------------------

To use the provider:

1. `Install-Package NHibernate.SqlAzure`
2. Set the `Database` to use `SqlAzureClientDriver` as the client driver, e.g.:

        Fluently.Configure()
            .Database(MsSqlConfiguration.MsSql2008.ConnectionString(connectionString).Driver<SqlAzureClientDriver>())
3. Set the `Environment.ConnectionProvider` property of the session factory configuration to `typeof(SqlAzureDriverConnectionProvider).AssemblyQualifiedName)`, e.g.:

        Fluently.Configure()
            ...
            .ExposeConfiguration(c => c.SetProperty(Environment.ConnectionProvider, typeof(SqlAzureDriverConnectionProvider).AssemblyQualifiedName))


Using the provider when using an XML configuration
--------------------------------------------------

To use the provider:

1. `Install-Package NHibernate.SqlAzure`
2. Set the `connection.driver_class` property on the session factory configuration to `NHibernate.SqlAzure.SqlAzureClientDriver, NHibernate.SqlAzure`
3. Set the `connection.provider` property on the session factory configuration to `NHibernate.SqlAzure.SqlAzureDriverConnectionProvider, NHibernate.SqlAzure`

Running the tests
-----------------

If you want to contribute to this library then you need to:

1. Load the solution (allow the NuGet package restore to grab all the packages)
2. Compile the solution (.NET 4, AnyCPU)
3. Create a database on your local SQLExpress instance called `NHibernateSqlAzureTests` and grant the user running the NUnit runner `dbowner` access.
    * If you want to use a different database simply change the `Database` ConnectionString in `App.config`
4. Run the `NHibernate.SqlAzure.Tests` project with your NUnit test runner of choice

