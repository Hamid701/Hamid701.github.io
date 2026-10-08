---
title: "Can AI Help Maintain a Turbofan Engine?"
permalink: /portfolio/turbofan-maintenance-copilot/
excerpt: "<img src='/images/turbofan-engine-hero.jpg' alt='Cutaway side view of an IHI XF9-1 prototype turbofan engine' style='float:right; margin:10px; width:400px; border-radius:20px;'> <br/> Aircraft maintenance teams spend valuable time moving between long manuals and separate sensor reports. I built a retrieval-augmented generation (RAG) copilot that returns source-backed maintenance guidance and an engine-life estimate in one place. As an illustrative business case, saving 10 to 20 minutes across 20 research tasks each week could recover roughly 170 to 350 technician hours per team each year. This is an approximation, not measured production savings. <br/><br/> <a class='btn btn--info' href='https://github.com/Hamid701/turbofan-maintenance-copilot' target='_blank' rel='noopener'>View on GitHub</a>"
collection: portfolio
header:
  teaser: turbofan-engine-hero.jpg
---

<div class="project-case-study" markdown="1">

<section class="case-hero">
  <div>
    <p class="case-eyebrow">AI for maintenance decision support</p>
    <h2>Maintenance answers that can be checked.</h2>
    <p>Aircraft maintenance information is spread across long manuals, while an engine's condition is hidden inside streams of sensor readings. I built a retrieval-augmented generation (RAG) copilot that brings those two sources together.</p>
    <p>Users can ask a question in plain language, inspect the handbook pages behind the answer, and estimate how many operating cycles an engine may have left.</p>
    <div class="case-actions">
      <a class="btn btn--info" href="https://turbofan-copilot-wspib53mua-ew.a.run.app/" target="_blank" rel="noopener">View live interface</a>
      <a class="btn btn--light-outline" href="https://github.com/Hamid701/turbofan-maintenance-copilot" target="_blank" rel="noopener">View source code</a>
    </div>
  </div>
  <figure class="case-hero__image">
    <img src="/images/turbofan-engine-hero.jpg" alt="Cutaway side view of an IHI XF9-1 prototype turbofan engine">
    <figcaption>IHI XF9-1 prototype turbofan cutaway. Photo by <a href="https://commons.wikimedia.org/wiki/File:IHI_XF9-1_prototype_turbofan_engine_(cutaway_model)_left_side_view_in_IHI_booth_of_JA2024_at_Tokyo_Big_Sight_October_19,_2024.jpg" target="_blank" rel="noopener">Hunini / Wikimedia Commons</a>, licensed under <a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank" rel="noopener">CC BY-SA 4.0</a>.</figcaption>
  </figure>
</section>

<aside class="case-impact-note">
  <strong>Approximate business impact</strong>
  <p>If the copilot saves 10 to 20 minutes across 20 maintenance research tasks per week, one team could recover roughly <strong>170 to 350 technician hours per year</strong>. At a rough staff cost of €50 to €100 per hour, that represents about <strong>€9,000 to €35,000 in annual time value</strong>. This scenario is directional, not a measured production result. It excludes downtime, safety, certification, and implementation costs.</p>
</aside>

## Why I built it

Maintenance decisions sit at the intersection of documentation, engine data, and human judgement. Each source is useful, but moving between them makes a simple investigation slower than it needs to be.

<div class="case-grid">
  <div class="case-card">
    <span class="case-card__number">1</span>
    <h3>Manuals are precise</h3>
    <p>Official handbooks contain the right guidance, but finding the relevant page can take time.</p>
  </div>
  <div class="case-card">
    <span class="case-card__number">2</span>
    <h3>Sensors tell a story</h3>
    <p>Changes in temperature, pressure, and vibration can reveal deterioration before a failure.</p>
  </div>
  <div class="case-card">
    <span class="case-card__number">3</span>
    <h3>Answers need evidence</h3>
    <p>A confident response is not enough. The user should be able to inspect its source and limits.</p>
  </div>
</div>

## From question to checkable answer

<figure class="case-figure">
  <picture>
    <source media="(max-width: 780px)" srcset="/images/turbofan-copilot-flow-mobile.svg">
    <img src="/images/turbofan-copilot-flow.svg" alt="Four steps: ask a maintenance question, find relevant handbook pages, add engine data when requested, and return a source-backed answer">
  </picture>
  <figcaption>The copilot combines handbook guidance with engine information while keeping the evidence visible.</figcaption>
</figure>

The experience is intentionally simple. A user asks a normal question, such as what should be inspected when an engine shows a worsening temperature trend. The application finds relevant maintenance guidance, adds sensor-based information when an engine is named, and returns one combined response.

## How the RAG pipeline works

RAG stands for **retrieval-augmented generation**. Instead of asking a language model to answer from memory alone, the application first searches an approved maintenance library and places the most relevant evidence beside the question. The model then writes its response from that evidence.

<div class="case-rag-grid">
  <div class="case-rag-step">
    <span class="case-rag-step__number">1</span>
    <h3>Retrieve in two ways</h3>
    <p>A keyword search finds exact technical terms, while BGE semantic embeddings find passages with similar meaning. Both search the same 1,050 page-grounded handbook passages.</p>
  </div>
  <div class="case-rag-step">
    <span class="case-rag-step__number">2</span>
    <h3>Combine the rankings</h3>
    <p>Reciprocal Rank Fusion merges both result lists and selects the five strongest passages. This hybrid approach performed best at placing a relevant result first.</p>
  </div>
  <div class="case-rag-step">
    <span class="case-rag-step__number">3</span>
    <h3>Generate from evidence</h3>
    <p>GPT-4o-mini receives the question and retrieved passages through a structured prompt. If the evidence does not support an answer, the pipeline returns a refusal.</p>
  </div>
  <div class="case-rag-step">
    <span class="case-rag-step__number">4</span>
    <h3>Rebuild the citations</h3>
    <p>The model selects passage numbers, but the application maps them back to stored source and page metadata. Citations are reconstructed by code rather than written by the model.</p>
  </div>
</div>

Engine-health figures follow a separate path: sensor trends and remaining useful life are calculated by numerical code and a trained prediction model. The language model may explain those results, but it does not invent or calculate them.

## What makes the answer useful

<div class="case-trust-grid">
  <div class="case-card">
    <h3>Sources stay visible</h3>
    <p>Each maintenance answer points back to the exact FAA handbook page used to produce it.</p>
  </div>
  <div class="case-card">
    <h3>Engine figures stay separate</h3>
    <p>Sensor trends and remaining-life estimates come from numerical models, not from invented AI prose.</p>
  </div>
  <div class="case-card">
    <h3>It can say “I don't know”</h3>
    <p>Unsupported or unrelated questions, including attempts to override its rules, are refused instead of answered confidently.</p>
  </div>
</div>

## Measured results

<div class="case-stats">
  <div class="case-stat">
    <span class="case-stat__value">67%</span>
    <span class="case-stat__label">lower average prediction error</span>
    <p>On the NASA FD001 test set, average remaining-life error fell from 25.8 to 8.4 cycles.</p>
  </div>
  <div class="case-stat">
    <span class="case-stat__value">10/10</span>
    <span class="case-stat__label">small safety test</span>
    <p>The system answered supported questions and declined unsupported questions or attempts to override its rules.</p>
  </div>
  <div class="case-stat">
    <span class="case-stat__value">1,050</span>
    <span class="case-stat__label">searchable handbook passages</span>
    <p>Three selected FAA Powerplant Handbook chapters retain their original page references.</p>
  </div>
</div>

<figure class="case-figure">
  <picture>
    <source media="(max-width: 780px)" srcset="/images/turbofan-rul-improvement-mobile.svg">
    <img src="/images/turbofan-rul-improvement.svg" alt="Bar chart showing average remaining-life prediction error decreasing from 25.8 cycles for the original baseline to 8.4 cycles for the final model">
  </picture>
  <figcaption>Average absolute error on 100 held-out NASA FD001 engines using the project's capped-target evaluation. Lower is better.</figcaption>
</figure>

These are engineering evaluation results, not evidence of operational savings or aviation certification. The question-answering checks are deliberately small, and the engine model was tested on one simulated operating condition and one fault mode.

## The live application

<figure class="case-figure">
  <img src="/images/turbofan-copilot-interface.png" alt="The deployed Turbofan Maintenance Copilot interface with suggested handbook and engine-health questions">
  <figcaption>The deployed interface. API access is protected, so portfolio visitors can view the application without receiving a public credential.</figcaption>
</figure>

The interface provides example questions for both kinds of work: handbook research and engine-health analysis. It also displays the decision-support warning before a user submits anything.

<aside class="case-access-note">
  <div>
    <strong>Want to test the copilot?</strong>
    <p>The live interface is public, but asking questions requires an API key so usage and cost remain controlled. Email me and I will provide a temporary key for testing.</p>
  </div>
  <a class="btn btn--info" href="mailto:ettayyebi.hamid@gmail.com?subject=Turbofan%20Copilot%20API%20key">Request an API key</a>
</aside>

## Technical stack

This is an end-to-end application rather than a standalone model demo. The stack covers document retrieval, predictive maintenance, a secured web API, automated testing, and cloud observability.

<figure class="case-figure case-architecture">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="/images/turbofan-architecture-dark.svg">
    <img src="/images/turbofan-architecture-light.svg" alt="Architecture diagram showing a question moving through routing, hybrid handbook retrieval, engine analysis, grounded OpenAI generation, reconstructed citations, PostgreSQL storage, and monitoring">
  </picture>
  <figcaption>The production architecture. Retrieval, engine analytics, generation, citation reconstruction, and monitoring remain separate so each result can be inspected.</figcaption>
</figure>

<div class="case-stack-grid">
  <section class="case-stack-card">
    <p class="case-stack-card__eyebrow">RAG &amp; language AI</p>
    <h3>Hybrid search with grounded generation</h3>
    <p>Lexical and semantic retrieval are fused before a structured OpenAI response is produced. Embeddings run locally on CPU, while PostgreSQL keeps the text, vectors, and source metadata together.</p>
    <div class="case-stack-tags">
      <span>GPT-4o-mini</span><span>BGE-small</span><span>ONNX Runtime</span><span>pgvector</span><span>LangChain Core</span>
    </div>
  </section>
  <section class="case-stack-card">
    <p class="case-stack-card__eyebrow">Predictive maintenance</p>
    <h3>Sensor-based remaining-life estimation</h3>
    <p>A gradient-boosted model uses 30-cycle windows of NASA C-MAPSS sensor data to estimate remaining useful life and report its typical test error.</p>
    <div class="case-stack-tags">
      <span>scikit-learn</span><span>pandas</span><span>NumPy</span><span>NASA C-MAPSS</span>
    </div>
  </section>
  <section class="case-stack-card">
    <p class="case-stack-card__eyebrow">Application &amp; data</p>
    <h3>A typed, secured Python service</h3>
    <p>FastAPI exposes normal and progress-streaming endpoints. Pydantic validates every response, while SQLAlchemy and Alembic manage the PostgreSQL data layer.</p>
    <div class="case-stack-tags">
      <span>Python 3.13</span><span>FastAPI</span><span>Pydantic</span><span>PostgreSQL</span><span>SQLAlchemy</span>
    </div>
  </section>
  <section class="case-stack-card">
    <p class="case-stack-card__eyebrow">Quality &amp; operations</p>
    <h3>Tested and observable in production</h3>
    <p>The container is deployed to Google Cloud Run with managed secrets. Langfuse traces the RAG pipeline, and cloud metrics expose latency, failures, question volume, and estimated cost.</p>
    <div class="case-stack-tags">
      <span>Docker</span><span>Cloud Run</span><span>Langfuse</span><span>Pytest</span><span>Ruff</span><span>mypy</span>
    </div>
  </section>
</div>

<div class="case-two-column">
  <div>
    <h2>Designed to be checked, not simply believed</h2>
    <ul class="case-checklist">
      <li><strong>Page references are reconstructed from retrieved passages.</strong> The language model cannot make up a citation that the application then presents as real.</li>
      <li><strong>Predictions include their typical error.</strong> The user sees that remaining useful life is an estimate, not a known future value.</li>
      <li><strong>Questions and outcomes are monitored.</strong> This makes failures, refusals, response time, and cost visible after deployment.</li>
      <li><strong>The service is protected by an API key.</strong> The public portfolio does not expose a credential.</li>
    </ul>
  </div>
  <aside class="case-limit">
    <h3>Limits matter</h3>
    <p>This is a portfolio research system, not certified maintenance guidance. It uses selected handbook chapters rather than the full maintenance library. Its engine model uses NASA's simulated FD001 dataset, and its reported error is an average across a test set rather than a guarantee for an individual engine.</p>
  </aside>
</div>

## What I learned

The most important lesson was that an AI application is more than the model that writes the final paragraph. The difficult work is deciding what the model may control, which facts must come from deterministic calculations, how a user verifies the evidence, and how failures become visible after deployment.

This project brought together information retrieval, predictive maintenance, API development, testing, monitoring, security, and cloud deployment as one working product. It also reinforced a principle I want to carry into future AI work: a useful system should make uncertainty easier to understand, not hide it behind confident language.

<section class="case-cta">
  <h2>Explore the project</h2>
  <p>The complete repository contains the evaluation results, architecture, tests, deployment setup, and documented limitations.</p>
  <div class="case-actions" style="justify-content:center;">
    <a class="btn btn--info" href="https://github.com/Hamid701/turbofan-maintenance-copilot" target="_blank" rel="noopener">Open GitHub repository</a>
    <a class="btn" href="https://github.com/Hamid701/turbofan-maintenance-copilot/blob/main/docs/threat-model.md" target="_blank" rel="noopener">Read the threat model</a>
  </div>
</section>

</div>
