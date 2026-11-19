# otel-todo

Express todo service backed by MongoDB, traced with OpenTelemetry and viewed in Jaeger. This is CIS4930 A9.

## Run it

1. Start Docker, then Mongo and Jaeger:

```
docker run -d -p 27017:27017 mongo
docker run -d --name jaeger -p 16686:16686 -p 4317:4317 -p 4318:4318 -p 5778:5778 -p 9411:9411 jaegertracing/jaeger:2.5.0
```

2. Install and start the server:

```
npm install
node --require ./tracing.js index.js
```

3. Hit the route a few times:

```
curl http://localhost:3000/todo
```

4. Open http://localhost:16686, pick `todo-service` in the search panel and look at the traces.

Spans go to Jaeger through the OTLP exporter in `tracing.js`. Metrics still print to the console.
