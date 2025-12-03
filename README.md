<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Basetwo AI | Manufacturing CoPilot on Google Cloud</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta
    name="description"
    content="Basetwo is an AI CoPilot for manufacturing that runs on Google Cloud, helping process engineers optimize yield, quality, and costs."
  />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap"
    rel="stylesheet"
  />
  <style>
    :root {
      --bg: #f5f7fb;
      --bg-alt: #ffffff;
      --accent: #2563eb;
      --accent-soft: rgba(37, 99, 235, 0.08);
      --accent-strong: #1d4ed8;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --border-subtle: #e2e8f0;
      --chip-bg: #e0edff;
      --shadow-soft: 0 18px 40px rgba(15, 23, 42, 0.12);
      --radius-xl: 18px;
      --radius-xxl: 24px;
      --transition-fast: 160ms ease-out;
      --layout-max-width: 1120px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: "Inter", system-ui, -apple-system, BlinkMacSystemFont,
        "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #e0ecff 0, #f5f7fb 45%, #f9fafb 100%);
      color: var(--text-main);
      line-height: 1.6;
      padding: 0;
      margin: 0;
    }

    a {
      color: var(--accent);
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

    .page {
      max-width: var(--layout-max-width);
      margin: 0 auto;
      padding: 32px 20px 56px;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 32px;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-mark {
      width: 32px;
      height: 32px;
      border-radius: 12px;
      background: conic-gradient(
        from 180deg,
        #1d4ed8,
        #22c55e,
        #0ea5e9,
        #a855f7,
        #1d4ed8
      );
      display: flex;
      align-items: center;
      justify-content: center;
      color: #f8fafc;
      font-size: 18px;
      font-weight: 700;
      box-shadow: 0 10px 25px rgba(37, 99, 235, 0.45);
    }

    .logo-text-main {
      font-weight: 650;
      letter-spacing: 0.02em;
      font-size: 18px;
    }

    .logo-text-sub {
      font-size: 11px;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.12em;
    }

    .tagline {
      display: none;
    }

    @media (min-width: 720px) {
      .tagline {
        display: block;
        font-size: 13px;
        color: var(--text-muted);
      }
    }

    /* Hero */
    .hero {
      display: grid;
      grid-template-columns: minmax(0, 3fr) minmax(0, 2.4fr);
      gap: 28px;
      align-items: stretch;
      margin-bottom: 32px;
    }

    @media (max-width: 860px) {
      .hero {
        grid-template-columns: 1fr;
      }
    }

    .hero-left {
      background: linear-gradient(145deg, #ffffff, #e9f0ff);
      border-radius: var(--radius-xxl);
      padding: 28px 26px;
      box-shadow: var(--shadow-soft);
      position: relative;
      overflow: hidden;
    }

    .hero-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 5px 12px;
      border-radius: 999px;
      background: rgba(15, 118, 110, 0.06);
      border: 1px solid rgba(148, 163, 184, 0.4);
      font-size: 12px;
      color: #0f766e;
      margin-bottom: 14px;
    }

    .hero-pill span {
      padding: 3px 7px;
      border-radius: 999px;
      background: #ecfdf5;
      font-weight: 600;
      color: #047857;
    }

    h1 {
      font-size: 30px;
      line-height: 1.16;
      margin-bottom: 8px;
      letter-spacing: -0.03em;
    }

    .hero-subtitle {
      font-size: 14px;
      color: var(--text-muted);
      margin-bottom: 20px;
      max-width: 460px;
    }

    .hero-metrics {
      display: flex;
      flex-wrap: wrap;
      gap: 16px;
      margin-bottom: 22px;
    }

    .metric {
      padding: 10px 14px;
      border-radius: 14px;
      background: rgba(15, 23, 42, 0.04);
      border: 1px solid rgba(148, 163, 184, 0.5);
      min-width: 120px;
    }

    .metric-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--text-muted);
      margin-bottom: 4px;
    }

    .metric-value {
      font-weight: 650;
      font-size: 17px;
    }

    .metric-note {
      font-size: 11px;
      color: var(--text-muted);
    }

    .hero-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      align-items: center;
    }

    .btn-primary {
      border: none;
      background: linear-gradient(135deg, var(--accent), var(--accent-strong));
      color: #f9fafb;
      font-weight: 600;
      padding: 10px 18px;
      border-radius: 999px;
      font-size: 13px;
      box-shadow: 0 14px 35px rgba(37, 99, 235, 0.48);
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: transform var(--transition-fast), box-shadow var(--transition-fast),
        background-position 160ms ease-out;
      background-size: 170% 170%;
      background-position: 0 50%;
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 18px 40px rgba(37, 99, 235, 0.6);
      background-position: 100% 50%;
    }

    .btn-secondary {
      border-radius: 999px;
      padding: 8px 16px;
      border: 1px solid rgba(148, 163, 184, 0.9);
      background: rgba(15, 23, 42, 0.02);
      color: var(--text-main);
      font-size: 13px;
      font-weight: 500;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      transition: background var(--transition-fast), transform var(--transition-fast),
        box-shadow var(--transition-fast);
    }

    .btn-secondary:hover {
      background: rgba(15, 23, 42, 0.04);
      transform: translateY(-1px);
      box-shadow: 0 8px 22px rgba(148, 163, 184, 0.4);
    }

    .hero-footnote {
      margin-top: 14px;
      font-size: 11px;
      color: var(--text-muted);
    }

    /* Right side card */
    .hero-right {
      display: flex;
      flex-direction: column;
      gap: 18px;
    }

    .card {
      background: var(--bg-alt);
      border-radius: var(--radius-xl);
      border: 1px solid var(--border-subtle);
      padding: 18px 18px 16px;
      box-shadow: 0 10px 28px rgba(15, 23, 42, 0.06);
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }

    .card-title {
      font-size: 14px;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .card-badge {
      padding: 4px 9px;
      border-radius: 999px;
      font-size: 11px;
      background: var(--chip-bg);
      color: #1d4ed8;
      font-weight: 500;
    }

    .card-body {
      font-size: 13px;
      color: var(--text-muted);
    }

    .chip-row {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: 10px;
    }

    .chip {
      font-size: 11px;
      padding: 5px 9px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.03);
      border: 1px solid rgba(148, 163, 184, 0.7);
      color: var(--text-main);
    }

    .chip.chip-gcp {
      background: var(--accent-soft);
      border-color: rgba(37, 99, 235, 0.5);
      color: var(--accent-strong);
      font-weight: 500;
    }

    /* Architecture diagram */
    .diagram {
      margin-top: 8px;
      border-radius: 14px;
      border: 1px dashed rgba(148, 163, 184, 0.7);
      padding: 10px;
      background: radial-gradient(circle at top left, #e0ecff, #ffffff);
      font-size: 11px;
    }

    .diagram-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px;
      align-items: start;
    }

    @media (max-width: 720px) {
      .diagram-grid {
        grid-template-columns: 1fr;
      }
    }

    .diagram-node {
      padding: 8px;
      border-radius: 10px;
      background: rgba(248, 250, 252, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.7);
    }

    .diagram-node-title {
      font-weight: 600;
      font-size: 11px;
      margin-bottom: 3px;
    }

    .diagram-node-body {
      font-size: 11px;
      color: var(--text-muted);
    }

    .diagram-arrow {
      text-align: center;
      font-size: 18px;
      color: rgba(148, 163, 184, 0.9);
      padding: 2px 0;
    }

    /* Sections */
    section {
      margin-top: 34px;
    }

    .section-heading {
      font-size: 18px;
      margin-bottom: 10px;
      letter-spacing: -0.02em;
    }

    .section-lead {
      font-size: 13px;
      color: var(--text-muted);
      max-width: 640px;
      margin-bottom: 16px;
    }

    .three-col {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 14px;
    }

    @media (max-width: 900px) {
      .three-col {
        grid-template-columns: 1fr;
      }
    }

    .feature {
      background: var(--bg-alt);
      border-radius: 16px;
      border: 1px solid var(--border-subtle);
      padding: 14px 14px 12px;
      font-size: 13px;
      box-shadow: 0 12px 25px rgba(15, 23, 42, 0.04);
    }

    .feature-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--text-muted);
      margin-bottom: 4px;
    }

    .feature-title {
      font-weight: 600;
      margin-bottom: 4px;
      font-size: 14px;
    }

    .feature-body {
      color: var(--text-muted);
      font-size: 13px;
    }

    .impact-grid {
      display: grid;
      grid-template-columns: 2fr 3fr;
      gap: 16px;
    }

    @media (max-width: 860px) {
      .impact-grid {
        grid-template-columns: 1fr;
      }
    }

    .impact-highlight {
      background: linear-gradient(145deg, #0f172a, #020617);
      color: #e5e7eb;
      border-radius: 18px;
      padding: 18px;
      box-shadow: 0 18px 40px rgba(15, 23, 42, 0.7);
      font-size: 13px;
    }

    .impact-highlight h3 {
      font-size: 16px;
      margin-bottom: 6px;
      letter-spacing: -0.02em;
    }

    .impact-number-row {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-top: 10px;
    }

    .impact-number {
      padding: 7px 11px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.6);
      font-size: 12px;
      font-weight: 500;
    }

    .impact-list {
      font-size: 13px;
      color: var(--text-muted);
      padding-left: 18px;
    }

    .impact-list li + li {
      margin-top: 4px;
    }

    footer {
      margin-top: 40px;
      padding-top: 16px;
      border-top: 1px solid rgba(148, 163, 184, 0.4);
      font-size: 11px;
      color: var(--text-muted);
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 10px;
    }

    footer strong {
      color: var(--text-main);
      font-weight: 600;
    }
  </style>
</head>
<body>
  <div class="page">
    <header>
      <div class="logo">
        <div class="logo-mark">B</div>
        <div>
          <div class="logo-text-main">Basetwo AI</div>
          <div class="logo-text-sub">Manufacturing CoPilot on Google Cloud</div>
        </div>
      </div>
      <div class="tagline">
        AI-driven optimization for complex manufacturing lines, powered by Vertex AI,
        BigQuery, and Cloud Run.
      </div>
    </header>

    <!-- Hero -->
    <main>
      <section class="hero">
        <div class="hero-left">
          <div class="hero-pill">
            <span>Solution Qualification</span>
            Verified on Google Cloud
          </div>
          <h1>AI CoPilot for high-value manufacturing, built on Google Cloud.</h1>
          <p class="hero-subtitle">
            Basetwo gives process engineers real-time recommendations on how to tune
            recipes, equipment, and operating conditions to optimize yield, cycle time,
            and cost across complex production lines.
          </p>

          <div class="hero-metrics">
            <div class="metric">
              <div class="metric-label">Measured impact</div>
              <div class="metric-value">&gt; 20% cost reduction</div>
              <div class="metric-note">
                In scale-up time and operational spend for Fortune 500 manufacturers.
              </div>
            </div>
            <div class="metric">
              <div class="metric-label">Deployment model</div>
              <div class="metric-value">Cloud-native SaaS</div>
              <div class="metric-note">
                Hosted on Google Cloud with enterprise-grade security and governance.
              </div>
            </div>
          </div>

          <div class="hero-actions">
            <button class="btn-primary" onclick="scrollToSection('architecture')">
              View Google Cloud architecture →
            </button>
            <button class="btn-secondary" onclick="scrollToSection('use-cases')">
              Explore manufacturing use cases
            </button>
          </div>

          <p class="hero-footnote">
            Basetwo combines physics-based models with machine learning so engineers can
            test changes virtually before they touch the production floor.
          </p>
        </div>

        <aside class="hero-right">
          <div class="card">
            <div class="card-header">
              <div class="card-title">
                Google Cloud integration
              </div>
              <span class="card-badge">Vertex AI • BigQuery • Cloud Run</span>
            </div>
            <div class="card-body">
              Basetwo connects plant-level data sources to Google Cloud, where models
              are trained, deployed, and governed at scale.
              <div class="chip-row">
                <span class="chip chip-gcp">Vertex AI Pipelines &amp; Workbench</span>
                <span class="chip chip-gcp">BigQuery manufacturing data mart</span>
                <span class="chip chip-gcp">Cloud Run inference services</span>
                <span class="chip">Cloud Storage data lake</span>
                <span class="chip">Cloud Logging &amp; Monitoring</span>
              </div>
            </div>
          </div>

          <div class="card">
            <div class="card-header">
              <div class="card-title">High-level architecture</div>
            </div>
            <div class="diagram">
              <div class="diagram-grid">
                <div class="diagram-node">
                  <div class="diagram-node-title">Plant data sources</div>
                  <div class="diagram-node-body">
                    Historians, MES, LIMS, ERP, and IoT sensors stream structured and
                    time-series data into Google Cloud via secure connectors.
                  </div>
                </div>

                <div class="diagram-node">
                  <div class="diagram-node-title">Google Cloud data &amp; ML</div>
                  <div class="diagram-node-body">
                    Data lands in Cloud Storage and BigQuery; Vertex AI hosts hybrid
                    physics + ML models; Cloud Run exposes low-latency optimization APIs.
                  </div>
                </div>

                <div class="diagram-node">
                  <div class="diagram-node-title">Basetwo CoPilot UI</div>
                  <div class="diagram-node-body">
                    Engineers explore scenarios, review model-driven insights, and push
                    validated set-points back to the plant through governed workflows.
                  </div>
                </div>
              </div>
              <div class="diagram-arrow">⇢</div>
              <div class="diagram-node">
                <div class="diagram-node-title">Security &amp; governance</div>
                <div class="diagram-node-body">
                  IAM-based access control, VPC-secured connectivity, encryption in
                  transit and at rest, regional data residency, and full audit logging.
                </div>
              </div>
            </div>
          </div>
        </aside>
      </section>

      <!-- Overview -->
      <section id="overview">
        <h2 class="section-heading">What Basetwo solves for manufacturers</h2>
        <p class="section-lead">
          Modern production environments generate massive volumes of data, but
          engineering teams still rely on spreadsheets, trial-and-error experiments,
          and tribal knowledge to debug and optimize processes. Basetwo turns raw data
          into guided recommendations on Google Cloud.
        </p>
        <div class="three-col">
          <div class="feature">
            <div class="feature-label">Challenge</div>
            <div class="feature-title">Complex, multivariate processes</div>
            <div class="feature-body">
              High-value processes span dozens of variables and tight tolerances.
              Small changes ripple across quality, yield, and throughput, making manual
              optimization slow and risky.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Approach</div>
            <div class="feature-title">Hybrid physics + ML models</div>
            <div class="feature-body">
              Basetwo blends first-principles models with ML trained in Vertex AI to
              accurately capture process behavior, test what-if scenarios, and
              recommend optimal set-points before changes are deployed.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Outcome</div>
            <div class="feature-title">Faster, data-driven decisions</div>
            <div class="feature-body">
              Engineers move from reactive firefighting to proactive, simulation-driven
              decision-making, shortening scale-up cycles and unlocking sustainable cost
              savings.
            </div>
          </div>
        </div>
      </section>

      <!-- Architecture focus -->
      <section id="architecture">
        <h2 class="section-heading">Reference architecture on Google Cloud</h2>
        <p class="section-lead">
          Basetwo is implemented as a secure, multi-tenant SaaS platform on Google
          Cloud. The diagram below highlights the core services and how they work
          together to deliver the CoPilot experience.
        </p>
        <div class="three-col">
          <div class="feature">
            <div class="feature-label">Data &amp; integration</div>
            <div class="feature-title">BigQuery &amp; Cloud Storage</div>
            <div class="feature-body">
              Plant data from historians, MES, and lab systems is ingested into Cloud
              Storage and organized into curated BigQuery datasets for analytics,
              feature engineering, and long-term retention.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Model lifecycle</div>
            <div class="feature-title">Vertex AI platform</div>
            <div class="feature-body">
              Vertex AI Workbench and Pipelines orchestrate data prep, training, and
              evaluation of hybrid models. Models are deployed to Vertex AI Endpoints
              for low-latency scoring or packaged into containers running on Cloud Run.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Serving &amp; security</div>
            <div class="feature-title">Cloud Run, IAM &amp; logging</div>
            <div class="feature-body">
              Optimization and recommendation services are exposed via Cloud Run
              microservices secured with IAM and VPC Service Controls. Cloud Logging,
              Cloud Monitoring, and audit logs provide full traceability and SRE
              visibility.
            </div>
          </div>
        </div>
      </section>

      <!-- Use cases -->
      <section id="use-cases">
        <h2 class="section-heading">Representative use cases</h2>
        <p class="section-lead">
          Basetwo is used by Fortune 500 manufacturers in chemicals, pharma, and
          advanced materials to de-risk technology transfer and optimize ongoing
          operations.
        </p>
        <div class="three-col">
          <div class="feature">
            <div class="feature-label">Use case #1</div>
            <div class="feature-title">Scale-up &amp; tech transfer</div>
            <div class="feature-body">
              Simulate recipe and equipment changes in Basetwo before moving from pilot
              to commercial scale. Engineers compare predicted yield and variability
              across scenarios, reducing experimentation time and scrap.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Use case #2</div>
            <div class="feature-title">Continuous process optimization</div>
            <div class="feature-body">
              For continuous lines, Basetwo monitors live signals, detects drift, and
              surfaces next-best actions to operators, such as adjusting residence
              time, feed rates, or temperatures within defined constraints.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Use case #3</div>
            <div class="feature-title">Energy &amp; sustainability</div>
            <div class="feature-body">
              By jointly modeling product quality and energy consumption, Basetwo helps
              teams hit sustainability KPIs—such as reduced emissions per unit of
              output—without compromising throughput or quality.
            </div>
          </div>
        </div>
      </section>

      <!-- Impact -->
      <section id="impact">
        <h2 class="section-heading">Proven business impact</h2>
        <div class="impact-grid">
          <div class="impact-highlight">
            <h3>Fortune 500 deployment outcomes</h3>
            <p>
              Across multiple large-scale deployments, Basetwo has helped global
              manufacturers realize measurable, production-grade value within months of
              rollout.
            </p>
            <div class="impact-number-row">
              <span class="impact-number">▲ &gt; 20% reduction in scale-up time</span>
              <span class="impact-number">▲ &gt; 20% reduction in operating costs</span>
              <span class="impact-number">▼ fewer off-spec batches &amp; scrap events</span>
            </div>
          </div>
          <ul class="impact-list">
            <li>
              <strong>Faster onboarding of new lines and products.</strong>
              Process knowledge is encoded into models, making it easier to replicate
              best-known configurations across plants.
            </li>
            <li>
              <strong>More resilient operations.</strong>
              Engineers receive guided, explainable recommendations instead of raw
              anomaly alerts, enabling faster decisions during excursions.
            </li>
            <li>
              <strong>Designed for regulated industries.</strong>
              Data residency, encryption, and detailed audit logs support compliance
              requirements in pharma and other tightly regulated verticals.
            </li>
          </ul>
        </div>
      </section>

      <!-- Contact / footer -->
      <section id="contact">
        <h2 class="section-heading">Learn more or request a manufacturing demo</h2>
        <p class="section-lead">
          Basetwo AI is headquartered in Canada and works with manufacturing teams
          globally. To discuss how this Google Cloud-based CoPilot can be applied to
          your specific processes, reach out to us.
        </p>
        <div class="three-col">
          <div class="feature">
            <div class="feature-label">Contact</div>
            <div class="feature-title">Basetwo AI</div>
            <div class="feature-body">
              Email:
              <a href="mailto:kiefer@basetwo.me">kiefer@basetwo.me</a><br />
              Website:
              <a href="https://basetwo.me" target="_blank" rel="noreferrer"
                >https://basetwo.me</a
              >
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Solution status</div>
            <div class="feature-title">Launched SaaS offering</div>
            <div class="feature-body">
              Cloud-hosted solution with active deployments at Fortune 500
              manufacturers. Available for proof-of-concepts and production rollouts on
              Google Cloud.
            </div>
          </div>
          <div class="feature">
            <div class="feature-label">Primary Google products</div>
            <div class="feature-title">Vertex AI, BigQuery, Cloud Run</div>
            <div class="feature-body">
              Basetwo primarily leverages Vertex AI for model lifecycle management,
              BigQuery for analytics, and Cloud Run for scalable inference, with Cloud
              Storage, Cloud Logging, and IAM providing the foundation.
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer>
      <div>
        © <span id="year"></span> <strong>Basetwo AI</strong>. All rights reserved.
      </div>
      <div>
        Built as a reference solution page for
        <strong>Google Cloud Partner &mdash; Solution Qualification</strong>.
      </div>
    </footer>
  </div>

  <script>
    // Smooth scroll to sections
    function scrollToSection(id) {
      var el = document.getElementById(id);
      if (!el) return;
      window.scrollTo({
        top: el.getBoundingClientRect().top + window.scrollY - 60,
        behavior: "smooth",
      });
    }

    // Set current year in footer
    document.getElementById("year").textContent = new Date().getFullYear();
  </script>
</body>
</html>
