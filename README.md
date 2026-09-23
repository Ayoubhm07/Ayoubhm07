### Ayoub Hammoudi

Software engineer — full-stack and AI platforms. I ship systems end to end, and I measure before I claim.
Based in Paris, available for full-time roles from February 2027.

---

#### Open source

Nothing below is merged yet; each line says where it stands.

- **[apache/iceberg-python#4003](https://github.com/apache/iceberg-python/issues/4003)** — *issue, open.*
  Above 200 values in an `IN` predicate, PyIceberg turns off file pruning: a delete then plans 20 of 20 data files
  instead of 1, rewrites the same single file, and reads the other 19 for nothing. One key more, twenty times the I/O.
  Shipped with a 40-line reproducer, a 240-run benchmark with medians and dispersion, a control experiment that rules
  out predicate size, and the 2020 Java commit that introduced the guard.
- **[apache/iceberg-python#4004](https://github.com/apache/iceberg-python/pull/4004)** — *PR, under review.*
  `In` / `NotIn` built their literal set twice: 200,000 objects for 100,000 distinct values. Predicate construction is
  42% faster at 100,000 values. Reviewed by a maintainer, revised, and the revision also fixes a silent bug where a
  predicate built from a generator came out empty — a filter that matched nothing, with no error.
- **[huggingface/huggingface.js#2510](https://github.com/huggingface/huggingface.js/pull/2510)** — *PR, open.*
  A `@huggingface/hub` test assumed the platform supported symlinks instead of detecting the capability. It failed on
  Windows and was invisible to an Ubuntu-only CI.
- **[NVIDIA/garak#2217](https://github.com/NVIDIA/garak/issues/2217)** — *issue, open, independently reproduced.*
  English-only detectors misjudge a target that answers in another language, in **both** directions: a French refusal
  scores as a successful attack, and French toxic content scores clean. False positives are visible; false negatives
  are not. Discussion with the maintainers is open on whether this belongs in core or behind a flag.

#### Projects

- **[AFTERSHOCK](https://github.com/Ayoubhm07/Aftershock)** — real-time seismic lakehouse.
  USGS events through an idempotent Kafka (KRaft) producer into Spark Structured Streaming, Delta tables on HDFS in
  bronze/silver/gold, four Airflow DAGs chained by Datasets, replay after a hard kill proven to write no duplicates.
  It measures something nobody archives: of 2,128 earthquakes tracked across their full version history, 735 (34.5%)
  had their magnitude revised after publication — the number that triggered the alert was not the final one.
- **[Taintrace](https://github.com/Ayoubhm07/Taintrace)** — sanctions screening over a Bitcoin contamination graph.
  OFAC and OpenSanctions ingested by Airflow as streams without disk writes, Bitcoin screened over Kafka, taint
  propagated over *n* hops in Neo4j, the whole chain running as containerized services that start with one command. Traced 512.25 BTC received by an address on no sanctions list, 11.07% tainted at
  three hops — the case regulators care about and a single-hop check misses.
- **[AI for Molecular Design](https://github.com/Ayoubhm07/AI-for-Molecular-Design-)** — machine learning for
  EGFR drug discovery, solo. Eight notebooks from ChEMBL acquisition to classification, pIC50 regression,
  clustering and activity cliffs, every model compared against a simple baseline. The companion Next.js site
  computes molecular properties and similarity through a cheminformatics engine written in Rust and compiled to
  WebAssembly, with a live in-browser benchmark against the JavaScript path and an automatic fallback when the
  WebAssembly fails to load.

- **Phantera** — LLM outbound platform, solo-built, pre-launch (private).
  Durable orchestration on Inngest with deduplication by event key in Redis, Stripe usage-based billing, and a CI gate
  built on an LLM evaluation harness (F1, MAE, Spearman) with NVIDIA garak red-teaming and prompt-injection detection.

#### How I work

- I benchmark with repetitions, medians and dispersion, never a single run — and I throw away a series when the
  control says the machine drifted. One of the Iceberg series went in the bin for exactly that reason.
- I write down what I did **not** prove. The Iceberg issue says plainly that I could not reproduce the reporter's
  1054 s, and that the fix does nothing for uniformly spread keys.
- I kill my own ideas when the code disagrees. A second optimisation looked like a 4x win until I read `Literal.to`
  closely: it bounds values rather than converting them, so the shortcut would have made pruning wrong. It is out.

#### Working with

Python · TypeScript · Java · event-driven microservices (Fastify, NestJS, Spring Cloud, API gateways, Keycloak) ·
Kafka · Spark Structured Streaming · Airflow · Delta Lake · Apache Iceberg · Neo4j · PostgreSQL · MongoDB · Redis ·
Next.js · React · Docker · Playwright · LLM evaluation and red-teaming

[Portfolio](https://ayoubdevspace.vercel.app/) · [LinkedIn](https://www.linkedin.com/in/ayoub-hammoudi-3251851b8/)
