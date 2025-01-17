```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

```mermaid
graph TD;
andthen{andThen}-->and;
and{and}-->ineq2{!=};
ineq2-->lag(lag);
lag-->speed1(Speed);
ineq2-->zero2(0);
and-->eq1{=};
eq1-->speed2(Speed);
eq1-->zero3(0);
andthen-->windowed((Windowed<br>90 sec))
windowed-->ineq1{!=};
windowed-->total((Total time<br> < 60 sec));
ineq1-->oilpump(OilPump);
ineq1-->zero1(0);

style lag fill:#f9f
style zero1 fill:#9ff
style zero2 fill:#9ff
style zero3 fill:#9ff
style speed1 fill:#ff9
style speed2 fill:#ff9
style oilpump fill:#ff9
style windowed fill:#9f9
style total fill:#99f
```

```mermaid
graph TD;  

  %% Top level
  TSP --> Front
  TSP --> Core
  TSP --> DSL
  TSP --> Integration
  TSP --> QA
  
  %% Datapath
  Front --> Kafka(Kafka<br>Consumer)
  Kafka --> Parquet(Parquet<br>Decoder)
  Parquet --> Pandas(Pandas<br>Decoder)
  Pandas --> Clover(Clover<br>Decoder)

  %% HTTP
  Front --> http(HTTP<br>service)

  %% JDBC
  Front --> JDBC(JDBC<br> Doobie)
  JDBC --> Postgre(PostgreSQL<br>Doobie)
  JDBC --> WrapInflux(InfluxDB<br>Doobie)
  JDBC --> WrapCH(Clickhouse<br>Doobie)
  WrapInflux --> Influx(InfluxDB<br>Native)
  WrapCH --> ClickHouse(ClichkHouse<br>Native)

  %% Core
  Core --> CoreWrap(ZIO Wrap)
  CoreWrap --> CoreMonad(Core<br>Monad)
  Core --> Parallelism

  %% DSL
  DSL --> WrapDSL(ZIO Wrap)
  WrapDSL --> DslMonad(DSL<br>Monad);
  
  %% Styling

  %% Ready
  style Kafka fill:#9f9
  style Parquet fill:#9f9

  %% Early Stage
  style Pandas fill:#ff9
  style CoreWrap fill:#ff9

  %% Late Stage
  style http fill:#f99
    
  %% Reused
  style CoreMonad fill:#f9f
  style DslMonad fill:#f9f
  
```
