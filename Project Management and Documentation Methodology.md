# Final Document — MOU Clause 4.6: Project Management and Documentation Methodology

---

## LaTeX Body

```latex
\section{Executive Summary}\label{sec:exec_sum}

This document establishes the project management, progress tracking, and
source code documentation methodology for joint industry--academic
collaborative research projects conducted between Vector Omega (Pvt) Ltd
and the University of Moratuwa (UOM). In compliance with Clause~4.6 of
the Memorandum of Understanding (MOU), all project operations, data
handling, and development lifecycles are governed by internationally
accepted standards---specifically \textbf{ISO~21502:2020}
\cite{iso21502_2020}, \textbf{ISO/IEC/IEEE~12207:2017}
\cite{iso_iec_ieee_12207_2017}, and \textbf{ISO~9001:2015}
\cite{iso9001_2015}.

The framework is deliberately project-agnostic: it defines the
\emph{process} by which any collaborative project shall be managed and
documented, without prescribing the technical content of any individual
project. Each project initiated under the MOU will inherit these
procedures as its baseline operating methodology.


\section{Introduction}\label{sec:intro}

Research and development initiatives operate under inherent ambiguity.
Traditional linear project management frameworks are highly vulnerable
to single points of failure in these settings, as they are poorly
adapted to the creative exploration, iterative hypothesis testing, and
frequent pivoting that characterise complex research
\cite{marle2015limits, Jetter2015}. A failed experiment under a linear
plan can halt an entire programme; under a portfolio-based plan, it
becomes a documented learning that redirects resources toward more
promising avenues \cite{wingate2025project}.

To mitigate these execution risks, the proposed methodology adopts a
systematic \emph{portfolio architecture} \cite{liao2003knowledge}
managed via objective \emph{phase-gate reviews}
\cite{cooper2010stage, cooper2017idea, iso21502_2020}. Rather than
detailing the granular technical aspects of individual research projects,
this document instructs the Project Committee on the Standard Operating
Procedures (SOPs) governing project execution. These SOPs are
deliberately designed to guarantee:

\begin{enumerate}
    \item \textbf{Systematic traceability}: every experimental decision, dataset, and source code modification is tracked using strict configuration management and version-controlled systems \cite{iso_iec_ieee_12207_2017, iso9001_2015}.
    \item \textbf{Transparent review mechanisms}: all developmental progress is subject to structured, cross-functional milestone reviews at designated phase-gates \cite{cooper2010stage, iso21502_2020}.
    \item \textbf{Verifiable progress evaluation}: objective readiness-check criteria and scoring rubrics explicitly govern all resource allocation and project continuation decisions \cite{cooper2017idea, iso21502_2020}.
\end{enumerate}

To ensure that every developmental phase---from initial discovery
through final industrial production---remains entirely auditable,
peer-reviewable, and scientifically rigorous, the project lifecycle is
explicitly anchored to the normative baselines provided by
\textbf{ISO~21502:2020} \cite{iso21502_2020},
\textbf{ISO/IEC/IEEE~12207:2017} \cite{iso_iec_ieee_12207_2017}, and
\textbf{ISO~9001:2015} \cite{iso9001_2015}.


\section{Project Management Mechanism}\label{sec:pm}

\subsection{Portfolio Architecture and Track-Based Execution}

The research programme is decoupled into independent, concurrent
\emph{Research Tracks} (e.g., data acquisition, algorithm development,
system integration). This portfolio architecture provides resilience
against the single-track vulnerabilities that plague linear R\&D plans
\cite{wingate2025project}:

\begin{itemize}
    \item \textbf{Parallel Execution:} Multiple tracks operate
          concurrently. A blocker or negative result in one track does
          not stall the broader initiative.
    \item \textbf{Sprint-Based Progress:} Execution within each track
          is managed in defined two-week sprints, enabling the
          Project Committee to monitor progress at regular, predictable
          intervals \cite{iso21502_2020}.
    \item \textbf{Dynamic Resource Allocation:} Resources are
          dynamically shifted toward tracks demonstrating the highest
          viability, maximising both academic output and industrial
          deliverables.
\end{itemize}

\subsection{Stage-Gate Decision Model}

To enforce rigorous project governance, every proposed research activity
must pass through sequential decision gates. This model is adapted from
Cooper's Stage-Gate\textsuperscript{\textregistered} system
\cite{cooper2010stage, cooper2017idea} and aligns with the continued
justification and viability assessment principles of ISO~21502
\cite{iso21502_2020}:

\begin{description}
    \item[Gate~0 --- Discovery:] Validates alignment with core
         academic and industrial research questions.
    \item[Gate~1 --- Scoping:] Assesses technical feasibility and
         ensures resource availability.
    \item[Gate~2 --- Go/No-Go:] Utilises a weighted scoring rubric
         evaluating strategic alignment, technical feasibility, and
         expected impact before resources are committed.
    \item[Gate~3 --- Mid-Review:] Evaluates ongoing execution against
         predefined milestones and acceptance criteria.
    \item[Gate~4 --- Completion:] Formally verifies learning outcomes,
         triggering publication and knowledge-capture workflows.
\end{description}

Regular progress review meetings are institutionalised as part of the
core communication strategy \cite{iso21502_2020}. All review meetings
yield formal minutes and tracked action items, forming an unbroken chain
of evidence demonstrating how research decisions were made, how risks
were mitigated, and how academic feedback was systematically integrated
into the project trajectory \cite{iso9001_2015}.


\section{Result Documentation and Source Code Management}\label{sec:docs}

\subsection{Source Code Configuration and Traceability}

To satisfy Clause~4.6 of the MOU regarding source code documentation,
the software development lifecycle strictly adheres to the configuration
management protocols defined in ISO/IEC/IEEE~12207:2017
\cite{iso_iec_ieee_12207_2017}:

\begin{itemize}
    \item \textbf{Semantic Version Control:} All source code, firmware,
          algorithms, and trained models are managed via strict Git
          workflows, creating an immutable, timestamped ledger of all
          technical contributions. This guarantees full visibility into
          the software's evolution from prototype to mature product.

    \item \textbf{Conventional Commits:} Every alteration to the
          codebase is accompanied by a standardised, human- and
          machine-readable commit message (e.g., \texttt{feat:},
          \texttt{fix:}, \texttt{docs:}, \texttt{refactor:})
          \cite{conventionalcommits}. This practice directly supports
          configuration status accounting requirements
          \cite{iso_iec_ieee_12207_2017}, enabling the Project Committee
          to programmatically parse project history, evaluate the
          velocity of development phases, and trace the genesis of
          specific algorithms.

    \item \textbf{Branching Taxonomy:} Strict repository naming
          conventions separate R\&D exploration from production-ready
          code. Legacy techniques and experimental deviations are
          preserved in designated archive branches (e.g.,
          \texttt{archive/manual-scale-calibration}), ensuring
          experimental reproducibility while preventing codebase
          pollution \cite{iso9001_2015}.
\end{itemize}

\subsection{Post-Execution Documentation}

Upon conclusion of each experimental activity, results are formally
captured in two complementary registers:

\begin{itemize}
    \item \textbf{Experiment Reports:} Comprehensive summaries
          containing outcomes, statistical interpretations, and direct
          links to generated datasets and code repositories.

    \item \textbf{Dead-End Registry:} Approaches that fail to yield
          expected results are documented with rigorous root-cause
          analysis. In applied research, confirmed negative results hold
          equal epistemic value to successful ones, preventing future
          cohorts from duplicating ineffective efforts
          \cite{liao2003knowledge}.
\end{itemize}

\subsection{Data Integrity and FAIR Compliance}

All research data is managed in accordance with the FAIR Guiding
Principles for scientific data management \cite{wilkinson2016fair}:

\begin{itemize}
    \item \textbf{Findable:} Every dataset is assigned a persistent
          identifier and annotated with rich metadata.
    \item \textbf{Accessible:} Data is retrievable via standard
          protocols with documented access conditions.
    \item \textbf{Interoperable:} Standard data formats and metadata
          schemas are enforced across all projects.
    \item \textbf{Reusable:} Clear licensing, detailed provenance
          records, and version-controlled linkage between code and data
          ensure long-term reusability.
\end{itemize}

Raw data is treated as strictly immutable. All datasets and trained
models are versioned using Data Version Control (DVC), ensuring that
every experimental result is fully reproducible from its exact data
and code configuration.


\section{Alignment with International Standards}\label{sec:standards}

The mechanisms described above are explicitly engineered to comply with
the following internationally recognised standards:

\begin{table}[h]
\centering
\small
\begin{tabular}{p{3.8cm} p{4cm} p{5.5cm}}
\hline
\textbf{Standard} & \textbf{Scope} & \textbf{Implementation} \\
\hline
ISO~21502:2020 \cite{iso21502_2020} &
  Project, programme and portfolio management &
  Track-based portfolio architecture; stage-gate decision model;
  sprint-based progress reviews \\[6pt]

ISO/IEC/IEEE 12207:2017 \cite{iso_iec_ieee_12207_2017} &
  Software life cycle processes &
  Git-based configuration management; Conventional Commits for
  status accounting; branching taxonomy for traceability \\[6pt]

ISO~9001:2015 \cite{iso9001_2015} &
  Quality management systems &
  Document control via version-controlled repositories; mandatory
  peer review; non-conformance logging via Dead-End Registry;
  continuous improvement through retrospectives \\
\hline
\end{tabular}
\caption{Mapping of project methodology to international standards.}
\label{tab:standards}
\end{table}


\section{Review Mechanisms and Quality Assurance}\label{sec:qa}

The integrity of the collaborative venture relies on continuous
evaluation and quality assurance, mapped directly to the monitoring,
measurement, analysis and evaluation requirements of ISO~9001:2015
\cite{iso9001_2015}:

\begin{itemize}
    \item \textbf{Mandatory Peer Review:} All software merges are
          subject to mandatory pull-request (PR) reviews, requiring
          approval from designated technical leads prior to integration.
          This enforces a systematic peer-review mechanism analogous to
          academic publication standards, ensuring that poorly
          documented or fundamentally flawed contributions are
          intercepted before affecting the primary research trajectory.

    \item \textbf{Milestone Gate Reviews:} At each stage gate
          (Section~\ref{sec:pm}), the Project Committee formally
          evaluates progress against predefined acceptance criteria.
          These reviews produce documented minutes, action items, and
          go/no-go decisions that form a complete audit trail.

    \item \textbf{Controlled Experimental Environment:} By strictly
          isolating experimental branches from peer-reviewed production
          branches, the methodology provides a highly controlled
          environment in which academic supervisors can assess the
          quality, validity, and standard compliance of research outputs
          with confidence in the underlying procedural architecture.
\end{itemize}
```

---

## BibTeX Entries to Add

Add these two new entries to your existing bibliography. All other `\cite{}` keys already exist in your file.

```bibtex
@article{wilkinson2016fair,
  author  = {Wilkinson, Mark D. and Dumontier, Michel and Aalbersberg, IJsbrand Jan
             and Appleton, Gabrielle and Axton, Myles and Baak, Arie and Blomberg, Niklas
             and Boiten, Jan-Willem and da Silva Santos, Luiz Bonino and Bourne, Philip E.
             and others},
  title   = {The {FAIR} Guiding Principles for scientific data management and stewardship},
  journal = {Scientific Data},
  volume  = {3},
  pages   = {160018},
  year    = {2016},
  doi     = {10.1038/sdata.2016.18},
  publisher = {Nature Publishing Group}
}

@misc{conventionalcommits,
  author       = {{Conventional Commits Contributors}},
  title        = {Conventional Commits Specification v1.0.0},
  year         = {2024},
  url          = {https://www.conventionalcommits.org/en/v1.0.0/},
  note         = {Accessed: 2026-06-07}
}
```

---

## Citation Key Reference

All `\cite{}` keys used in the document and where they come from:

| Citation Key | Already in your file? | Source |
|---|---|---|
| `iso21502_2020` | ✅ Yes | ISO 21502:2020 |
| `iso_iec_ieee_12207_2017` | ✅ Yes | ISO/IEC/IEEE 12207:2017 |
| `iso9001_2015` | ✅ Yes | ISO 9001:2015 |
| `marle2015limits` | ✅ Yes | Marle & Vidal (2015) |
| `Jetter2015` | ✅ Yes | Jetter & Albar (2015) |
| `wingate2025project` | ✅ Yes | Wingate (2025) |
| `liao2003knowledge` | ✅ Yes | Liao (2003) |
| `cooper2010stage` | ✅ Yes | Cooper (2010) |
| `cooper2017idea` | ✅ Yes | Cooper (2017) |
| `wilkinson2016fair` | 🆕 **Add** | Wilkinson et al. (2016) |
| `conventionalcommits` | 🆕 **Add** | Conventional Commits spec |
