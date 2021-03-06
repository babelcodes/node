# LoopBack

[![LoopBack](https://github.com/strongloop/loopback-next/raw/master/docs/site/imgs/branding/Powered-by-LoopBack-Badge-\(blue\)-@2x.png)](http://loopback.io/)

> LoopBack is a highly-extensible, open-source Node.js framework to quickly create dynamic end-to-end REST APIs.


## Presentation

> About LoopBack version 4 (completely redesigned -- 09/09/2018)

Pros of the 4th version:

- Code is written in [TypeScript](http://babel.codes/TypeScript/)
- Support for [Unit tests](https://loopback.io/doc/en/lb4/Testing-your-application.html)

## Concepts

[Application](https://loopback.io/doc/en/lb4/Application.html)
  - The central class for setting up all of your module's components, controllers, servers and bindings. 
  - This class extends `Context` and provides the controls for starting and stopping its associated servers.
  - This class provides bindings and sugar functions for commonly used bindings, like `component`, `server` and `controller`
  - This class can be found at `/src/my-app.application.ts`
  - The `Application` class constructor also accepts an [ApplicationConfig](http://apidocs.loopback.io/@loopback%2fdocs/core.html#ApplicationConfig)

[Context](https://loopback.io/doc/en/lb4/Context.html)
- An abstraction of states and dependencies in your application that LoopBack uses to manage everything.
- It’s a global registry for everything in your app (configurations, state, dependencies, classes and so on).
- An inversion of control container used to inject dependencies into your code
- Context instances can be chained using the parent to form a hierarchy, and an optional name.
- An application typically has three “levels” of context: application-level, server-level and request-level.
- Application-level context (global):
  - Stores all the initial and modified app state throughout the entire life of the app (while the process is alive)
  - Generally configured when the application is created 
  - `const app = new Application(); // 'app' is a "Context"`
- Server-level context:
  - Is a child of application-level context
  - Holds configuration specific to a particular server instance
  - Each server instance has the application-level context as its parent => any bindings defined on the application will also be available to the server(s)
- Request-level context:
  - Dynamically created for each incoming server request
  - Extend the application level context available through `this.ctx`
  - Are garbage collected once the response is sent
- _Bind_ via `ContextKey` and `ContextValue` 
- Consumers have to know the the type associated with each binding key (important because the bugs can be subtle and difficult to spot)
  - `export const HOST = new BindingKey<string | undefined>('rest.host');`
- See [Context API Docs](http://apidocs.loopback.io/@loopback%2fdocs/context.html) for more details

```
const app = new Application();
app.bind('hello').to('world'); // ContextKey='hello', ContextValue='world'
console.log(app.getSync<string>('hello')); // => 'world'
```

### TODO
- Server: An implementation for inbound transports/protocols such as REST (http, https), gRPC (http2) and graphQL (http, https). It typically listens on a specific endpoint (protocol/host/port), handles incoming requests, and then returns appropriate responses.

- Context

- Dependency Injection: The technique used to separate the construction of dependencies of a class or function from its behavior to keep the code loosely coupled.

- Controller: A class that implements operations defined by the application’s REST API. It implements an application’s business logic and acts as a bridge between the HTTP/REST API and domain/database models. A Controller operates only on processed input and abstractions of backend services / databases.

- Route: The mapping between your API specification and an Operation. It tells LoopBack which Operation to invoke() when given an HTTP request.

- Sequence: A stateless grouping of Actions that control how a Server responds to requests.

- Model: The definition of an object in respect to the datasource juggler. The @loopback/repository module provides special decorators for adding metadata to TypeScript/JavaScript classes to use them with the legacy implementation of DataSource Juggler. In addition, @loopback/repository-json-schema module uses the decorators’ metadata to build a matching JSON Schema.

- DataSources: A named configuration for a Connector instance that represents data in an external system.

- Repository: A type of service that represents a collection of data within a DataSource.

- Relation: A mapping between two models which describes a real world link between them and exposes CRUD APIs based on the configuration.

- Decorator: The pattern used to annotate or modify your class declarations and their members with metadata.

- Component: A package that bundles one or more Loopback extensions.
  - See Using components and Creating components for more information.


## 1. Create project

- https://loopback.io/doc/en/lb4/Getting-started.html

```
npm i -g @loopback/cli
lb4 app
cd getting-started
npm start
```

And complete `.gitignore`


## 2. Create new controller

```
lb4 controller
```
