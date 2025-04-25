### 🔹 **Basic Level**

1. **What is Elasticsearch and how does it work?**  
   **Elasticsearch** is a distributed, RESTful search and analytics engine built on **Apache Lucene**. It stores data in JSON format and provides fast full-text search capabilities. It’s commonly used for **log analytics**, **monitoring**, and **search applications**.

2. **What is an index in Elasticsearch?**  
   An index is a collection of documents that share the same structure. It's like a **database in RDBMS**.

3. **What is a document in Elasticsearch?**  
   A document is a **JSON object** stored in an index, analogous to a row in a table.

4. **What is a node and a cluster in Elasticsearch?**  
   - A **node** is a single instance of Elasticsearch.  
   - A **cluster** is a group of nodes that store data collectively and provide distributed search capabilities.

5. **What are shards and replicas?**  
   - **Shards** allow Elasticsearch to scale horizontally by splitting data across multiple nodes.  
   - **Replicas** provide **high availability** and fault tolerance.

6. **What is Kibana, and how does it integrate with Elasticsearch?**  
   Kibana is the visualization layer for Elasticsearch data. It provides dashboards, charts, and a GUI for querying Elasticsearch.

7. **What is the ELK/Elastic Stack?**  
   - **E**lasticsearch  
   - **L**ogstash (data ingestion)  
   - **K**ibana (visualization)  
   - Often extended with **Beats** (lightweight agents)

8. **How does Elasticsearch handle schema?**  
   Elasticsearch uses **dynamic mapping** to detect and assign field types automatically, but you can define mappings explicitly.

9. **What is an analyzer in Elasticsearch?**  
   An analyzer breaks text into terms or tokens during indexing and querying. It controls **how text is interpreted**.

10. **What is the purpose of Logstash and Beats in the Elasticsearch stack?**  
   - **Logstash** processes, transforms, and ships logs.  
   - **Beats** are lightweight agents that send data to Logstash or Elasticsearch.

---

### 🔹 **Scenario-Based / Intermediate to Advanced**

11. **You notice that some logs are not appearing in Kibana. What steps would you take to troubleshoot?**  
   - Check if **Beats/Logstash** is running.  
   - Verify **pipeline filters** in Logstash.  
   - Look for **index patterns** in Kibana.  
   - Confirm if data is reaching Elasticsearch using the `_cat/indices` and `_search` API.

12. **Elasticsearch is consuming a lot of heap memory and crashing frequently. What could be wrong?**  
   - JVM heap too small or too large (50% of system RAM is ideal, max 32 GB).  
   - High **field cardinality** (e.g., too many unique terms).  
   - Uncontrolled indexing rate.  
   - Perform `hot_threads` analysis and optimize queries.

13. **You want to rotate and retain logs for 30 days. How would you set this up in Elasticsearch?**  
   - Use **Index Lifecycle Management (ILM)**.  
   - Create policies to move indices from **hot → warm → delete** phases.  
   - Define retention rules like `delete after 30 days`.

14. **Your Elasticsearch cluster is in a yellow state. What does it mean and how do you fix it?**  
   - **Yellow** means primary shards are active, but **some replicas are not assigned**.  
   - Check if all nodes are up.  
   - Ensure there are **enough nodes** to allocate replicas.  
   - Use `_cluster/health` and `_cat/shards`.

15. **How would you scale Elasticsearch in a production environment?**  
   - Scale **horizontally** by adding nodes.  
   - Separate **data**, **master**, and **ingest** roles.  
   - Use **shard rebalancing** and **index templates** to control index sizes.

16. **How would you secure an Elasticsearch cluster?**  
   - Use **Elastic Stack Security features** (authentication, TLS encryption).  
   - Enable **role-based access control (RBAC)**.  
   - Avoid exposing nodes directly; use a **reverse proxy (e.g., Nginx)**.  
   - Secure access with **API keys or service tokens**.

17. **You need to automate Elasticsearch deployment in AWS. What tools and practices would you use?**  
   - Use **Terraform** for infrastructure provisioning.  
   - Use **Ansible**/Helm charts for Elasticsearch setup.  
   - Use **Elastic Cloud** or **Open Distro** on EKS.  
   - Ensure persistent volumes and snapshots.

18. **Your logs show `circuit_breaking_exception`. What is it and how do you resolve it?**  
   This error occurs when Elasticsearch **limits memory usage** to avoid out-of-memory issues.  
   - Identify which circuit breaker (parent, fielddata, request).  
   - Tune `indices.breaker.total.limit` or optimize your query.  
   - Reduce fielddata usage or use keyword instead of text fields for aggregations.

19. **How would you back up and restore an Elasticsearch cluster?**  
   - Use the **Snapshot and Restore API**.  
   - Configure a **repository** (e.g., S3) using the `PUT _snapshot` API.  
   - Automate snapshots with cron or a curator job.

20. **You want to migrate logs from an old Elasticsearch cluster to a new one. What approaches can you use?**  
   - Use **reindex API** with `remote` option.  
   - Use **Logstash** to re-read old logs and push to new cluster.  
   - Or dump data using `elasticdump`.

---
