# Bagisto API Performance & Load Testing Suite

An automated backend performance testing suite designed to simulate high-density mobile application traffic against a local **Bagisto (Laravel-based)** e-commerce engine ecosystem. Built using Apache JMeter to analyze system limits, database endurance, and API routing stability under concurrent user stress.

## 2. Project Architecture & Setup
The testing suite targets the REST API endpoints exposed to the storefront mobile application layer. The backend runs on a localized Apache web server fueled by a customized MariaDB environment.

- **Backend Platform:** Bagisto E-Commerce Framework
- **Local Infrastructure:** XAMPP Engine (Windows Server Mode)
- **Database Tuning:** Optimized `my.ini` buffer pool handling (`max_connections=500`, `innodb_buffer_pool_size=256M`) to eliminate thread locks.

---

## 3. Performance Testing Metrics & Scenarios

The suite models **100 concurrent mobile app users** executing multi-loop storefront actions via the native HTTP Java Client.

### Test Configuration Array
| Method | Target Endpoint Task | Execution Metric Scope |
| :--- | :--- | :--- |
| **SETUP** | Global Headers Initialization | Injects REST headers (`Accept/Content-Type: application/json`) globally to isolate stateful pipelines. |
| **GET** | Categories Deep Mapping Data | Measures catalog nested array compilation limits over 500 parallel delivery routines. |
| **GET** | Global Product Catalog Retrieval | Monitors backend row rendering performance for massive data table lookups. |
| **GET** | Indexed Character Search Filter | Assesses query execution speed when filtering records via localized search loops (`?search=laptop`). |
| **POST** | Add to Cart / Session Store | Evaluates write performance. Bypasses CSRF token validation structures (`VerifyCsrfToken.php`) to isolate REST operations. |

---

## 4. Execution Metrics & Results Analysis

### Test Plan Parameters
- **Simulated Mobile Client Pools (Threads):** 100
- **Ramp-Up Profile Window:** 10 seconds
- **Loop Multiplier Factor:** 5
- **Total Transaction Data Points:** 2,000 requests

### Aggregate Performance Logs
| Metric Label | Value / Result |
| :--- | :--- |
| **Overall Execution Pass Rate** | **100% Functional Completion** |
| **Average Response Latency Window** | `9,859 ms` |
| **System Threshold Throughput** | `8.9 requests/second` |
| **Net Infrastructure Traffic Flow** | `192.30 KB/sec` |
| **Localized Load Stress Drop Rate** | `1.60%` *(Expected localized timeout drops under intense saturation)* |

---

## 5. Diagnostic Case Studies (Lessons Learned)

During the incremental development of this automation project, multiple backend constraints were safely triaged and resolved:
1. **URL Rewrite Fallbacks:** Fixed initial routing dropouts pointing to generic XAMPP landing indexes by explicitly injecting `index.php` routing anchors into the relative sampler paths.
2. **Stateful Session Bypassing:**
